---
title: A2 - Gray Hat/Red Hat Visualization
---

# Assignment 2: Gray Hat/Red Hat Visualization
In this assignment, you will explore the ethical dimensions of data visualization by creating two contrasting visualizations of the same dataset: one “gray hat,” prioritizing accuracy, transparency, and graphical integrity, and one “red hat,” deliberately using persuasive or manipulative techniques. Working with one of five politically charged datasets, you will experiment with visual encodings, produce iterative sketches, and develop high-fidelity final visualizations. For each version, you will also write a short rationale describing your design decisions.

## Background
It is tempting to think of data and data visualization as a neutral actor. An emphasis on a minimalist aesthetic — particularly through the use of clean, precise geometric lines — lends an air of objective, transparent reporting that masks visualization’s persuasive power. Given the growing ubiquity of visualization as a medium for recording, analyzing, and communicating data, we have a responsibility to examine how our design choices can influence the way a visualization is read, and what insights a reader walks away with.

In this assignment, we will grapple with these ethical concerns by visualizing a single dataset from two different perspectives: the "gray hat" and the "red hat." These terms draw from the concept of different approaches to information presentation. A gray hat approach emphasizes neutral, objective visualization practices that prioritize accuracy, transparency, and balanced representation of the data. This approach aligns with Edward Tufte's principles of graphical integrity, which emphasize that visualizations should present data honestly, maintain proportionality between data values and their visual representation, and avoid design elements that distort or obscure the underlying information. Gray hat visualizations seek to minimize bias and emotional manipulation, presenting information in a way that allows readers to form their own conclusions and emotional responses based on a clear, honest presentation of facts.

In contrast, a red hat approach represents visualizations that deliberately employ persuasive or manipulative techniques—whether for legitimate advocacy purposes or potentially malicious intentions. This approach may violate Tufte's principles of graphical integrity by using misleading scales, cherry-picking data ranges, employing disproportionate visual elements, or introducing decorative features that distract from or distort the data. Red hat visualizations may evoke specific emotions, guide readers toward particular conclusions, or even mislead audiences through strategic design choices that amplify specific emotional reactions while obscuring alternative interpretations of the data.

Both approaches have their place in different contexts—from scientific reporting that demands the graphical integrity Tufte advocates to advocacy work that seeks to inspire action through emotional engagement. However, red hat techniques become ethically problematic when they fundamentally compromise data integrity with malicious intent to deceive, exploit, or harm audiences. Understanding this distinction helps us become more critical consumers and creators of data visualizations, recognizing how adherence to or departure from principles of graphical integrity can shape not only what we think, but also how we feel about the data, and developing our ability to identify when visualizations may be misleading us for harmful purposes.

For this assignment, we will consider a gray hat visualization to adhere to Tufte’s principles of graphical integrity:
- The visualization is clear, accessible, and appropriately designed for the intended audience (often the general population)
- Any data transformations (e.g., filters, aggregations, calculations, etc.) are transparently documented and justified
- Data sources are clearly cited, including acknowledgment of potential limitations, biases, or uncertainties
- Visual elements (scales, proportions, colors) accurately represent the underlying data relationships
- The overall design prioritizes honest communication over persuasive impact

A red hat visualization, on the other hand, exhibits one or several characteristics that compromise integrity:
- Visual representations are intentionally inappropriate for the data type, overly complex, or unnecessarily cluttered to obscure clear interpretation
- Labels, axes, legends, and scales are misleading, disproportionate, or manipulated to distort data relationships
- Titles, captions, and annotations are deliberately skewed to influence viewer perception rather than accurately describe the data
- Data has been selectively filtered, cherry-picked, or processed in ways that misrepresent the broader dataset or underlying trends
- Sources, methodology, and data provenance are obscured, omitted, or misrepresented
- Design elements (color choices, visual metaphors, emotional imagery) are employed specifically to manipulate emotional responses rather than clarify information

While we might never aspire to create genuinely deceptive visualizations in our professional practice, temporarily adopting a red hat perspective serves an important pedagogical purpose: it helps us understand the full rhetorical power of visualization design, sharpens our ability to critically evaluate the visualizations we encounter daily, and makes us more conscious of the ethical implications of our own design choices. By exploring both approaches, we become better equipped to recognize and resist manipulative visual communication while strengthening our commitment to honest, effective data presentation.

## Datasets
You will be working with a single dataset: **choose _one_ from the five** listed below. These datasets are intentionally chosen to cover politically charged topics as these are typically the type of data where ethical visualization is important. Note that you do not have to visualize the entire dataset (i.e., you may choose a subset of the data to visualize) and that your two visualizations can focus on different aspects of the data (but they must come from the same dataset).

The five datasets are the following:

- [Greenhouse Gas Emissions 1990–2022.](https://data-explorer.oecd.org/vis?df[ds]=DisseminateFinalDMZ&df[id]=DSD_AIR_GHG@DF_AIR_GHG&df[ag]=OECD.ENV.EPI) The Organization for Economic Co-operation and Development (OECD) has compiled data for the emissions of all participating countries broken out by the pollutant (e.g., carbon monoxide, methane, etc.) and by different sources (e.g., energy, agriculture, etc.). The linked interface can be a little difficult to use, but you can access various slices of the data by either choosing alternate themes in the left-hand side menu, or by customizing the pollutants and variables in the dropdown menus in the main view.
- [Gender Equality Indicators 1960–2021.](https://github.com/light-and-salt/World-Bank-Data-by-Indicators/tree/master/gender) The World Bank tracks a number of different measures including fertility rate, literacy, employment and ownership of businesses, and wages to study the extent of gender equality around the world. The linked dataset curates a smaller subset of the [overall set](https://data.worldbank.org/indicator#gender) of gender indicators which you are welcome to use as well.
- [Civilian Complaints Against New York City Police Officers.](https://projects.propublica.org/datastore/#civilian-complaints-against-new-york-city-police-officers) This is a dataset compiled by ProPublica, an independent, nonprofit investigative journalism newsroom. It contains more than 12,000 civilian complaints filed against the NYPD, with demographic information about the complainant and officer, the category of the alleged misconduct, and the result of the complaint.
- [Gentrification and Demographic Analysis.](https://github.com/BuzzFeedNews/2020-02-gentrification) This is a dataset compiled by BuzzFeed News to understand gentrification, or how the character and demographics of neighborhoods change as more affluent people and business move in and potentially displace existing residents. The process of data collection, cleaning, and analysis is well-documented by the BuzzFeed News team, and be sure to read the [accompanying article](https://www.buzzfeednews.com/article/lamvo/gentrification-maps-white-black-people-neighborhoods) which contains important context and details.
- [Gun Deaths in America.](https://github.com/fivethirtyeight/guns-data) This repository contains the R scripts and CSV datasets associated with FiveThirtyEight’s [Gun Deaths in America](http://fivethirtyeight.com/gun-deaths/) project. We recommend working with [full.csv](https://github.com/fivethirtyeight/guns-data/blob/master/full_data.csv) and reading the project page to understand the methodology used to compile this dataset.

## Your Tasks
You will be visualizing your dataset from two perspectives: the gray hat and red hat. As a result, you will be generating **two static visualizations** – one for each hat. We construe “visualization” broadly (e.g., a single visualization may comprise several small multiple views). You are free to use any visualization technique and any visualization tool, including sketching. 

That being said, you should keep the implications of hand-drawn versus programmatically generated visualizations on feelings of authoritativeness in mind. You also do not need to use the same tools/techniques to generate both visualizations. You should carefully consider not only visual encoding decisions but also how you might transform your data (e.g., calculating new fields; grouping, binning, or aggregating data; log transforms; etc.), and what annotations and labels might help best convey the message from a particular perspective.

For each visualization, document your decisions (including any data transformations performed) and describe your rationale in a short write-up (no more than 4 paragraphs per visualization). Note that subtlety is part of the rubric for the red hat visualization, which means we will likely rely heavily on your write-up for grading this visualization in particular.

## Grading
The assignment score is out of a maximum of 10 points, evenly divided between your gray and red hat visualizations. Submissions that squarely meet the requirements (i.e., the “Satisfactory” column in the rubric below) will receive a score of 7. We will determine scores by judging the clarity of your gray hat visualization, the subtle deceptiveness of your red hat visualization, and the quality of the associated write-ups.

We will use the following rubric to grade your assignment. Note that rubric cells do not map exactly to specific point scores. They are only meant to give you an idea of the aspects that go into our grading of your visualizations. Similar to A1, we reserve the right to penalize any submissions with overly lengthy reflections; that do not engage with the provided datasets in meaningful ways, etc.

<table>
  <thead>
    <tr>
      <th>Hat</th>
      <th>Component</th>
      <th>Excellent</th>
      <th>Satisfactory</th>
      <th>Poor</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="4">Gray</td>
      <td>Marks &amp; Encodings</td>
      <td>All design choices are effective. The visualization can be read and understood effortlessly.</td>
      <td>Design choices are largely effective, but minor errors hinder comprehension.</td>
      <td>Ineffective mark or encoding choices are distracting or potentially misleading.</td>
    </tr>
     <tr>
      <td>Data Transformation</td>
      <td>More advanced transformations (e.g., additional calculations, aggregations) were used to extend the dataset in interesting or useful ways.</td>
      <td>Simple transforms (e.g., sorting, filtering) were primarily used.</td>
      <td>The raw dataset was used directly, with little to no additional transformation.</td>
    </tr>
    <tr>
      <td>Titles &amp; Labels</td>
      <td>Titles and labels helpfully describe and contextualize the visualization.</td>
      <td>Most necessary titles and labels are present, but they could provide more context.</td>
      <td>Many titles or labels are missing, or do not provide human-legible information.</td>
    </tr>
    <tr>
      <td>Write-Up</td>
      <td>Your write up is well-crafted and provides reasoned justification for all design choices.</td>
      <td>Most design decisions are described, but rationale could be explained at a greater level of detail.</td>
      <td>Missing or incomplete. Several design choices are left unexplained.</td>
    </tr>
    <tr>
      <td rowspan="4">Red</td>
      <td>Deceptiveness</td>
      <td>Visualization is misleading in at least 2 out of these 3 categories: marks/encodings, data transformation, titles/labels.</td>
      <td>Visualization is misleading in only 1 of these 3 categories: marks/encodings, data transformation, titles/labels.</td>
      <td>No red hat techniques were used.</td>
    </tr>
    <tr>
      <td>Subtlety</td>
      <td>The red-hat techniques used are very subtle and need close study to be identified even by seasoned visualization readers.</td>
      <td>The red-hat techniques cannot be detected at first glance but are still somewhat easy to identify.</td>
      <td>The red-hat techniques could be immediately identified.</td>
    </tr>
     <tr>
      <td>Visualization Design (marks, encodings, data transformations, title & labels)</td>
      <td>Aspects of the visualization design make it appear interesting and possibly trustworthy.</td>
      <td>An acceptable quality of visualization design. However, some aspects do not help convince the reader of its trustworthiness.</td>
      <td>Poor quality of visualization design does not convince the reader that the visualization is trustworthy. E.g., certain elements such as titles or legends are missing altogether.</td>
    </tr>
    <tr>
      <td>Write-Up</td>
      <td>Your write up is well-crafted and provides reasoned justification for all design choices, and especially the red-hat techniques you used.</td>
      <td>Most design decisions are described, but rationale could be explained at a greater level of detail.</td>
      <td>Missing or incomplete. Several design choices are left unexplained.</td>
    </tr>
     <tr>
      <td>Either / Both</td>
      <td>Creativity &amp; Originality</td>
      <td>You exceeded the parameters of the assignment, with original insights or a particularly engaging design.</td>
      <td>You met all the parameters of the assignment.</td>
      <td>You met most of the parameters of the assignment.</td>
    </tr>
  </tbody>
</table>

## Submission Details/Checklist
This is an individual assignment. **You may not work in groups.** Your completed assignment is due on **Friday, October 10, 11:59 pm ET**. 
Submit your assignment on Markus. Make sure to include the following:
- [ ]  Your gray hat visualization (and the accompanying write-up)
- [ ]  Your red hat visualization (and the accompanying write-up)

Once again, make sure your visualizations are sized for a reasonable viewing experience — readers should not have to zoom or scroll in order to effectively view any visualization!

## Tips and Inspiration
In past years, we’ve had many questions about what constitutes a red hat” technique and how obvious it needs to be. Indeed, it’s a tricky balancing act. For instance red hattedness” is not a strictly monotonic function as you can raise a reader’s suspicion by using too many red hat techniques all at once, by making outright mistakes, or by making the misleading intent too obvious to the reader. Similarly, having an unclear (or no) data question, or omitting titles, axes, or legends are more likely to hinder a reader’s overall ability to read or make sense of a visualization rather than mislead them or slant the message.

So how should you navigate this design tension?

- Consider targeted ways in which you might violate strategies for effective encoding we discussed in lecture. [You might also find these slides](https://vis.csail.mit.edu/classes/6.859/lectures/03-VisualEncodingDarkPatterns.pdf) on “dark encodings” to be a useful resource.
- Consider how rhetorical techniques and editorial layers are deployed in visualizations. [You might find this paper by Jessica Hullman](http://vis.csail.mit.edu/classes/6.859/readings/Hullman-VisualizationRhetoric) useful for exploring these concepts.
- The following academic articles might also give you some interesting insights:
  - [Frames and Slants in Titles of Visualizations on Controversial Topics. Ha-Kyung Kong, Zhicheng Liu, Karrie Karahalios. ACM CHI. 2018.](https://vis.csail.mit.edu/classes/6.859/readings/Kong-FramesAndSlantsInTitlesOfVisualizationsOnControversialTopics)
  - [Useful Junk? The Effects of Visual Embellishment on Comprehension and Memorability of Charts. Scott Bateman, Regan L. Mandryk, Carl Gutwin, Aaron Genest, David McDine, Christopher Brooks. ACM CHI. 2010.](https://vis.csail.mit.edu/classes/6.859/readings/Bateman-UsefulJunk)
  - [The Work that Visualization Conventions Do. Helen Kennedy, Rosemary Lucy Hill, Giorgia Aiello & William Allen. Information, Communication & Society. 2016.](https://vis.csail.mit.edu/classes/6.859/readings/Kennedy-TheWorkThatVisualizationConventionsDo)
For some more “inspiration”, look at how visualizations are being used to promote [COVID-19 skepticism on social media](https://vis.csail.mit.edu/covid-story/) (you may also want to optionally consult the [associated paper](https://vis.csail.mit.edu/classes/6.859/readings/Lee-ViralVisualizations) this article is based on).

## Acknowledgements
This assignment is heavily inspired by [a similar effort](https://niklaselmqvist.medium.com/teaching-ethics-for-visualization-b48e3ced84df) from Niklas Elmqvist at the University of Maryland, College Park and Arvind Satyanarayan at MIT. The terminology used in this assignment was inspired by Hanspeter Pfister at Harvard University.