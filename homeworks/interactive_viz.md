---
title: A4 - Interactive Visualization
---

# Assignment 4: Interactive Visualization
## Background
For this assignment, you will explore the issues involved in implementing interactive and animated visualizations. You will build a visualization that enables interactive exploration or storytelling of a dataset of your own choosing and deploy it on the web. Think of this assignment as a small-scale version of your final project.

This assignment has two goals: (1) we want you to gain familiarity implementing interaction and animation techniques for visualizations; (2) we want you to think carefully about the effectiveness of specific interaction and animation techniques for your chosen data domain. For example, the [zipdecode](https://www.benfry.com/zipdecode/) and [NameGrapher](https://namerology.com/baby-name-grapher/) applications apply the interactive technique of dynamic queries – first explored in the [HomeFinder](http://www.cs.umd.edu/hcil/spotfire/) application – to the problem of uncovering patterns in zip codes and baby names. Similarly, interaction and animation techniques have also been very effectively used for explorable explanations, including [Kernel Density Estimation (KDE)](https://mathisonian.github.io/kde/) and [machine learning concepts](http://www.r2d3.us/?from=@).

A critical challenge will be scoping the assignment such that you can complete it within approximately 2-3 weeks (any more time than this should ideally be spent working on your final projects). Focus on designing a limited yet compelling visualization that enables interactive exploration along a few critical dimensions, and then layer on additional complexity. The [NameGrapher](https://namerology.com/baby-name-grapher/) application is a nice example that uses a simple but elegant interaction design to enable engaging explorations. A tightly-focused, well-implemented interactive graphic is much preferred to a sprawling design that attempts too much!

## Team Registration
For this assignment, you should work in teams of **1-3 students** (half the size of the final project group). Although you may work individually, we **strongly encourage** you to form a team as this assignment asks more from you than the previous ones in roughly the same amount of time. If you are looking for project partners, please post to Piazza to find classmates with similar interests!

You should register your team on Markus as soon as you have formed a team and picked a dataset and no later than **Friday 10/17, 11:59 pm ET**. You should include a concise title for your interactive visualization.

After you submit the form, you should set up a GitHub repository to enable version control among your teammates. The final deployment of your interactive visualization should also be hosted on a GitHub page by one of your team members.

## Your Tasks
Design an interactive graphic (with any necessary animation techniques) to explore or understand a compelling question for a dataset of your own choosing. In order to determine what subset of the data and which interactive options are most promising, we encourage you to perform additional exploratory analysis. What aspects of the data reveal the most interesting discoveries or stories? Do not feel obligated to try to convey _everything_ about the data: focus on a compelling subset.

Your graphic must include interactions and animations that enable exploration or storytelling. Possible techniques include panning, zooming, brushing, details-on-demand (e.g., tooltips), dynamic query filters, and selecting different measures to display. You are free to also consider highlights, annotations, or other narrative features intended to draw attention to particular items of interest and provide additional context.

Implement your graphic in D3.js and deploy it to the web. You may use plug-ins for JS and D3 provided your graphic does not require customized server-side support; you should simply load data from a static data file or public web API.

You should use [GitHub pages](https://docs.github.com/en/pages) to host your visualization from your project repository. We recommend keeping everything (development files and website) in your `main` branch: either serve your website from the root folder or from the `/docs` folder. Your repo must also contain the (unobfuscated) source code for your visualization.

After you have implemented and deployed your interactive visualization, you will complete a write-up with the following components:
- **A rationale for your design decisions.** How did you choose your particular visual encodings, interaction, and animation techniques? What alternatives did you consider and how did you arrive at your ultimate choices?
- **An overview of your development process.** Describe how the work was split among the team members. Include a commentary on the development process, including answers to the following questions: Roughly how much time did you spend developing your application (in people-hours)? What aspects took the most time?

Remember to acknowledge all appropriate sources not just in your write-up but also directly on your visualization itself (including the source of your data, and any example visualization you drew inspiration from). The write-up should be no longer than **two pages long** (you are free to use your own spacing and font size conventions, but please be reasonable).

## Minimum Viable Prototype (Fri, 10/17)
You must have a minimum viable working prototype online by **Friday 10/17, 11:59 pm ET**. **Late days may _not_ be used to extend this deadline.** The prototype need not be feature-complete or fully polished, but it should demonstrate the core visual encoding, interactive, and/or animated ideas you wish to ultimately include.

Please submit your work on MarkUs. Your prototype should be accessible on GitHub pages with a URL of the form: `https://csc316-student.github.io/cool-interactive-vis/`.

## Tutorial Presentations and Peer Critique (Tues, 10/21)
During the tutorials on **Tuesday 10/21 (2:30pm ET)**, we will split the class into multiple parallel sessions to watch demos of your A4 work so far and conduct peer design critiques. Your team should create a **4-minute** video presentation (**due Monday 10/20, 11:59 pm ET** on Quercus as a URL to your presentation) that covers the following content:
1. (~1 min) A short introduction to your dataset and goals of your project: what is it that your visualization is trying to help a reader with, and why is it important?
2. (~1 min) A demonstration of your A4 project so far.
3. (~1-1.5 mins) A discussion of some of the key design decisions you’ve made so far (e.g., did you do any exploratory data analysis and did it reveal something interesting? Why did you pick these particular visual encodings, or interaction and animation techniques? What alternative ideas did you explore or are you considering? etc.).
4. (~30 secs) A brief list of questions that you would like your peers in the class to comment on as part of their critique.

After each presentation, we will have a 1-2 minute Q&A session. The video presentations do not need to be fancy, a Zoom screencast of the relevant materials and interactions with your visualizations is fine.

During this week, each of you will also be responsible for critiquing three projects. We will do this during the tutorial section for the week. For each project, we would like you to not only pay close attention to the video presentation but also spend some time interacting with the visualization itself. You should then compose a critique following the structure we’ve used in class (“I like… I wish… What if…?”) and cover the following concerns:

- **Visual Encodings.** Are expressive and effective visual encodings applied? How well do they reveal the most important features or trends of the underlying data? Is critical data easily seen, or is it unnecessarily “hidden” and only revealed in response to interaction? Is the target audience likely to understand the visualization?
- **Interaction & Animation Techniques.** Do the supported interaction and animation techniques enable more effective discovery of interesting trends, patterns, or outliers? Do they engage the viewer in a process of meaningful exploration or learning? Are they well-implemented, without notable performance issues or usability problems?
- **Design Quality.** Assess the overall design quality in terms of organization and presentation. Are elements appropriately titled or labeled? Is there appropriate spacing, layout, legible type, and other forms of design styling? Is it clear where to begin viewing/interacting with the design? Is the overall display confusing or cluttered? How successful is the prototype in meeting the intended goals?

Critiques should be detailed enough to be actionable but brief, and all three critiques will be due shortly before reading break begins, on **Friday 10/24, 11:59pm ET**. Critiques can be submitted on MarkUs. We will grade your critiques on how thoughtfully you’ve engaged with the team’s visualization, and how constructive and actionable your feedback is.

## Final Submission (Fri, 11/07)
Over the reading break, we will email you all the critiques your team received. You will then have until **Friday 11/07, 11:59 pm ET** to improve your project based on this feedback, as well as continue to implement and polish any features that did not make it for the MVP submission. You _may_ use late days to extend this deadline (but keep in mind that _all_ group members will have their late day quota decremented should you exercise this option).
Make your final submission on Markus. The final submission should consist of a complete working prototype (provided as a URL) and the writeup as detailed above. Your visualization should be accessible on GitHub pages using a URL of the form: `https://csc316-student.github.io/cool-interactive-vis/`.

## Grading
Your grade in this assignment will be broken down into three components:
#### The Visualization

The visualization is scored out of 15 points. Visualizations that squarely meet the requirements for the assignment will receive a score of 12 out of 15. Going beyond the call of duty can net additional points, for example:
- advanced interaction or animation techniques
- novel visualization elements
- effective multi-view coordination
- thoughtful and elegant graphic design
- insightful & engaging exploration or narrative experience

Point deductions will be made when projects suffer from:
- errors or broken features
- clearly ineffective visual encodings
- lack of exploratory or narrative interaction or animation techniques
- overly simplistic or distracting interaction or animation techniques
- confusing interface design
- incomplete or insufficient write-up

#### The Tutorial Presentation
Presentations will be graded on a 2-point scale as evaluated by one of your TA’s. We will consider how well you describe your dataset and motivations and how compelling the demonstration of your visualization was (e.g., did your demo have a narrative arc, did you highlight interesting insights your visualization helps uncover, etc.).

#### Peer Critique
Each critique you write will be worth a point, for a total of 3 points. We will assess how thoughtfully you’ve engaged with the visualization, and how constructive and actionable your feedback is. Fractions of a point will be deducted for critiques that are shallow or do not offer much constructive feedback.

## Submission Details/Checklist
Here is a submission checklist, arranged chronologically to help you keep on top of your work:

- [ ] Fri, October 10: Register your team (up to 3 students) on Markus and setup GitHub repo
- [ ] Fri, October 17: Deploy A4 prototype and submit URL to Markus
- [ ] Mon, October 20: 4-minute video presentation due on Quercus
- [ ] Tues, October 21: Tutorial presentation for peer feedback/critique
- [ ] October 24: Peer reviews (x3) due on Quercus
- [ ] Fri, Nov 7: Final submission (GitHub pages URL + Writeup)

Please make your final submission on Markus. Make sure to include the following:

- [ ] GitHub pages URL to your final deployed visualization.
- [ ] Your write-up for the interactive visualization project (max. 2 pages)

You may want to test your visualization on a few devices and browsers (we will use Chrome or Firefox in our evaluations) amongst your group members to ensure there are no technical issues in advance of the final submission deadline.