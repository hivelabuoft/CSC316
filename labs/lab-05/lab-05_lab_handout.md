---
title: Lab 5 Handout
---

# Lab 5 Handout

### Learning Objectives

- Understand how to use JS classes 
- Learn best practices how to combine JS classes and D3
- Know how to *link* multiple views with each other
- Understand the concept behind D3's brush component
- Understand the JS keyword *this* and the scope of execution
- Get a better understanding of *system design* and *code structure*


### Prerequisites

- You have read and **programmed** along with:
	- [https://scotch.io/tutorials/demystifying-es6-classes-and-prototypal-inheritance](https://scotch.io/tutorials/demystifying-es6-classes-and-prototypal-inheritance) (explanation of JS ES6 Classes with more examples)


In the last weeks you have learned the fundamentals of the JS library D3. You have also gained some implementation expertise during previous labs and homeworks. You should be comfortable with the major concepts and be able to implement common charts as well as interactive and more advanced visualizations with D3.

In this lab you will work on a new problem set. It is continuous, a bit longer than the usual activities, and it will give you a better understanding of *linked views* and *system design*.

We will provide a template and many additional code snippets so that your main tasks will focus on the structure and the event handling components. However, please make sure that you understand the code in the provided templates, and take your time to read through it!


## Data

**Purchases for Household Supplies in the UK**

In this lab you will work with a dataset that contains detailed annual statistics on family food and drink purchases in the UK.

We have already extracted the major information and created a JSON file with data between 1974 and 2013.

The JSON file is divided into two major arrays with objects: 

- ```years``` contain the average weekly spending on food and drinks in pence (GBX) per person
- ```layers``` also contain the average weekly spending, but separated into 21 different *food* categories

*JSON Structure:*

```javascript
{
	"years": [
		{ "Year": 1974, "Expenditures": 331.437 },
		...
		{ "Year": 2013, "Expenditures": 2986.373 }
	],
	"layers": [
		{
			"Year": 1974,
			"Milk and milk products excluding cheese": 29.228,
			"Cheese": 8.694,
			"Carcase meat": 44.479,
			"Non-carcase meat and meat products": 55.915,
			"Fish": 13.652,
			"Eggs": 11.429,
			"Fats": 14.537,
			....
		},
		{
			"Year": 1975,
			"Milk and milk products excluding cheese": 37.239,
			"Cheese": 10.377,
			...
		},
		...
	]
}

```

The data is part of the annual *Family Food Report*, it is published through UK's open government platform *gov.uk* and is updated every year. However, the dataset is not completely accurate and there is a lack of data in some areas. For example, alcoholic and soft drink figures appear for the first time in 1992, but we can assume that people have consumed these products before.

*Source: [https://www.gov.uk/government/statistical-data-sets/family-food-datasets](https://www.gov.uk/government/statistical-data-sets/family-food-datasets)*

## Template

This lab will bring you a step closer to implementing more complex visualizations which makes it necessary to adapt the way how we organize our application. However, the provided template is quite similar to previous labs and homeworks. It is based on Bootstrap and it contains a basic HTML structure, some CSS rules and pieces of JS code.

During this lab we will introduce a concept which will help you to structure a D3 project with multiple visualizations. For this reason, we will also describe the file structure in more detail. The main change is that each visualization is a separate JS object and the implementation of the different visualizations is moved into separate JS files.

[Template.zip](https://hivelabuoft.github.io/CSC316/labs/lab-05/Template.zip)


## Preview

*After implementing all tasks your visualization should look like this:*

![Lab 7 - Preview](assets/cs171-lab6-preview.gif?raw=true "Lab 7 - Preview")


## Conceptual and technical background

Thinking about the structure of your project early on can save you a lot of time and will make your implementation more robust, extensible and reusable.


### Files and folders

*The provided template is structured as follows:*

- **index.html** is the default file that appears when a user invokes your webpage. It should include a basic structure and placeholders for your visualizations. 
- **/js** contains the JS files for the visualization and external libraries (can be further sub-divided)
- **/data** contains the data files
- **/css** contains the stylesheet files


### Divide and conquer

You should always try to split a complex problem into smaller, easier-to-tackle sub-problems. Each sub-problem will be solved independently and afterwards integrated into the final system.

**Visualizations should be organized and structured into individual code components** and, if possible, implemented as flexible and reusable components. Therefore, we will organize each visualization as an object.

The visualization specific implementation should be done in object functions (called methods) and should follow this pipeline:

![Vis object](assets/cs171-week-06-vis-object.png?raw=true "Vis Object")


### Visualizations as classes (new to ES6!)


*The following example will give you a better understanding of these steps.*

We can define a class with the ```class``` keyword, followed by the name of the class. Notice, that when defining a new class, it is convention and best practice to use a capital letter as first letter, to distinguish between the class itself and (potentially) an instance of the class.
```javascript
// Create a new class
class BarChart {}
```

After defining a class, we can define ```class members``` such as the ```constructor```, other ```methods```, or ```properties``` that the class should have. This is code that should live within the curly brackets of the class, and make up the ```body``` of the class.

The ```contructor```  of a class is a method whose purpose is to initialize an instance of that class.  So whenever we create an instance of a class, the constructor of that class is invoked to initialize the object’s properties with received parameters or default values.

Here is an example of a constructor for our BarChart class example. Notice that we can define properties for the BarChart class by using the keyword ```this```:
 

```javascript

class BarChart {

	// Runs whenever a new BarChart instance is created
	constructor(parentElement, data) {
		this.parentElement = parentElement;
		this.data = data;
	
	}
}
```


Once we have defined a class, we can create an instance of this class by using the keyword ```new```, referencing the class we want to create an instance of, and passing in the arguments for the constructor. 

```javascript
// Create an object instance
let barchart = new BarChart("bar-chart-container", data);
```


We can also implement methods in a class simply by adding their definition to the body of the class definition:


```javascript

class BarChart {

	// Runs whenever a new BarChart instance is created
	constructor(parentElement, data) {
	...
	}
	
	initVis(){ ...}
	
}
```


The variables should be stored in the class by using the ```this``` keyword. We would recommend creating another variable (for example ```vis```) within methods to store the *this*-accessor. Otherwise the scope of ```this``` will change and it will cause undesirable side-effects:

```javascript
initVis(){
	let vis = this;
	
	vis.margin = { top: 20, right: 0, bottom: 60, left: 60 };

	vis.width = 800 - vis.margin.left - vis.margin.right;
  	vis.height = 400 - vis.margin.top - vis.margin.bottom;
  
  	vis.svg = d3.select("#" + vis.parentElement).append("svg")
		.attr("width", vis.width + vis.margin.left + vis.margin.right)
		...
}
```

At the end of ```initVis()``` we call the function ```wrangleData()``` to follow our implementation pipeline:

```javascript
initVis(){
	...
	
	vis.wrangleData();
}
```

It is quite usual that you have to process and prepare data (filter, aggregate, ...) for a visualization whenever the data changes or after a user interaction. The function ```wrangleData()``` should take the raw data and modify it in a way that it can be mapped to the screen afterwards (```updateVis()```):

```javascript
wrangleData(){
	let vis = this;

	// Filter example
	vis.displayData = vis.data.filter(function(d){
		return d.year > 2000;
	});
	
	// Draw visualization
	vis.updateVis();
}
```

You should already be familiar with the last part. The function ```updateVis()``` contains the D3 update pattern (*enter, update, exit*). We use the variable ```displayData``` that we have created in ```wrangleData()``` before:

```javascript
updateVis(){
	let vis = this;

	// Update domains
	vis.y.domain([0, d3.max(vis.displayData, function(d) { return d.price; })]);
	...
	
	// Draw the actual bar chart
	var bar = svg.selectAll(".bar")
      .data(data);
  
	bar.enter().append("rect")
		.attr("class", "bar")
		...
}

```

### Project overview

The previous example showed the implementation of a bar chart in an object-oriented way using ES6 classes. To follow the main divide-and-conquer concept (i.e., splitting up a complex problem into various sub-tasks) we should also apply this to the file structure of our project.

![Project Overview](assets/cs171-lab6-overview.png?raw=true "Project Overview")

We separate the visualization specific code into external files and create object instances in the file ```main.js```, which is the entry point of our application. For example, if we want to use the same data for multiple charts we have to load the data only once in *main.js*. Thereby, our code stays clean and understandable. 

This methodology will become very helpful for developing larger systems and more sophisticated interaction mechanisms.


### Stack Shape

As you have seen in the preview at the beginning of this lab, you have to create a stacked area chart to visualize the different categories of UK's household expenditures. Instead of calculating the coordinates of these layers manually you can use *d3.stack()* to generate a baseline value for each datum, so you can "stack" layers of data on top of each other.

And as a reminder from the previous lab: *The D3 shape methods have no direct visual output. They take data that you provide and re-map or otherwise transform it, thereby generating new data that is more convenient for a specific task.*

*Example:*

```javascript
// Example data
var data = [
                {
                    "Milk": 10, "Water": 4, "Year": 2015
                },
                {
                    "Milk": 12, "Water": 6, "Year": 2016
                },
                {
                    "Milk": 11, "Water": 7, "Year": 2017
                }
            ];

// Initialize shape function specifying keys
let stack = d3.stack()
	.keys(["Milk", "Water"]);

// Call shape function on the dataset
let stackedData = stack(data);

console.log(stackedData);
```

Have a look at the console output. The resulting stacked data is now an array with two values, with each value an array itself corresponding to each category: "Milk", and "Water". Each entry in a category array provides two numerical values and the associated data object(```series[0][0].data```). The numerical values correspond to the *baseline* value, and the *topline* values respectively. For example, the first entry for "Milk" is ```series[0][0]``` where ```series[0][0][0]``` is the baseline and ```series[0][0][1]``` is the topline. Notice that the baseline value is equal to the sum of all the y values in the preceding categories. The category *"Milk"* is our first category and starts at the bottom, which means that the baseline values are zero. 


### Stacked Area

To stack these categories visually, we can create *stacked bar charts* or *stacked area charts*. In this lab you will create a stacked area chart. But it should be easy to adopt the workflow to a bar chart.

You have already created an area chart (see *HW4 - Za'atari Refugee Camp*) and a line chart (see *HW5 - FIFA World Cup*) and you should know how to use the D3 path generator. The built-in ```d3.area()``` is ideally suited for the stacked area chart too. It just needs some slight modifications of the ```y0()``` and ```y1()``` parameters to consider the different baselines:

```javascript
// Basic: area
let areaBasic = d3.area()
	.curve(d3.curveCardinal)
	.x(d=> x(d.data.Year))
	.y0(height)
	.y1(d=>y(d[1]-d[0]));

// Extended: stacked area
let areaExtended = d3.area()
	.curve(d3.curveCardinal)
	.x(d=> x(d.data.Year))
	.y0(d=> y(d[0]))
	.y1(d=>y(d[1]));
```

*The d3.curveCardinal interpolation curve is optional and can be used to create smooth shapes.*

### Focus+Context via Brushing

In the next task you will extend the visualization with a second chart (a basic area chart; see *Preview*), to give the user the possibility to zoom and to select a specific time range. 

#### Focus+Context

- The stacked area chart should show selected regions in greater detail (*focus*)
- The basic area chart preserves a global view at reduced detail without layers (*context*)

*This technique allows us to show the user detailed information linked with an overview (context) simultaneously.*

#### Brushing & Linking

The idea of *brushing* is to allow the user to select a subset of data interactively. In combination with *linking* - changes are automatically reflected in *linked* visualizations - you can get the desired focus+context visualization.

![Focus + Context](assets/cs171-week-06-focus-context.gif?raw=true "Focus + Context")


#### Brushing with D3

D3 Wiki: [https://github.com/d3/d3-brush/blob/master/README.md](https://github.com/d3/d3-brush/blob/master/README.md)

There are three types of brushes in D3 for brushing along the x, y dimensions, or both: d3.brushX, d3.brushY, and d3.brush. Each brush defines a selection in screen coordinates. The brushable area is specified via ```brush.extent()```.

The property **```on```** must be used to set an event listener, whereby you can choose between three different events:

- ```brushstart``` - on mousedown
- ```brush``` - on mousemove, if the brush extent has changed
- ```brushend``` - on mouseup

```javascript
// Initialize time scale (x-axis)
let xScale = d3.scaleTime()
	.range([0, width])
	.domain(d3.extent(displayData, function(d) { return d.Year; }));

// Initialize brush component
let brush = d3.brushX()
    .extent([[0, 0], [vis.width, vis.height]])
    .on("brush", brushed);
    
```

We can react to the *event* and update the linked visualizations in a separate function. Particularly noteworthy is the function ```d3.brushSelection(node)``` which returns the current brush extent or in other words, it returns the user's selection. 

```javascript
function brushed() {
	// Get the extent of the current brush
	let selectionRange = d3.brushSelection(d3.select(".brush").node());
	
	// Convert the extent into the corresponding domain values
	let selectionDomain = selectionRange.map(xScale.invert);
	
	// Update focus chart (detailed information)
	...
}
```

Note that we used ```d3.select(".brush").node()``` to specify which node's selection we want via a class attribute *brush*. In the last step it is necessary to append the brush to the *context chart* with the class attribute. This step is also comparable to appending a D3 axis. An additional rectangle, within the SVG group element, should indicate the current selection for the user: 

```javascript
// Append brush component
svg.append("g")
      .attr("class", "x brush")
      .call(brush)
    .selectAll("rect")
      .attr("y", -6)
      .attr("height", height + 7);
```

&nbsp;

**Resources**

- p. 273-281 in *D3 - Interactive Data Visualization for the Web* by Scott Murray
- [http://javascriptplayground.com/blog/2012/04/javascript-variable-scope-this/](http://javascriptplayground.com/blog/2012/04/javascript-variable-scope-this/)
- [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Introduction_to_Object-Oriented_JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Introduction_to_Object-Oriented_JavaScript)
- [http://www.w3schools.com/js/default.asp](http://www.w3schools.com/js/default.asp)
