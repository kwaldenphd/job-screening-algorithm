# Building a Job Screening Algorithm in Python

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>
This tutorial is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

## Lab Goals

## Acknowledgements

This lab is based on Evan Peck's "Ethical Design in CS 1: Building Hiring Algorithms" module. 
- Evan Peck, "[Ethical Design in CS 1: Building Hiring Algorithms in 1 Hour](https://medium.com/bucknell-hci/ethical-design-in-cs-1-building-hiring-algorithms-in-1-hour-41d8c913859f)" *Bucknell HCI, Medium blog* (28 March 2018)
- Evan Peck, "[Ethical Hiring Algorithms](https://ethicalcs.github.io/modules/hiring/)" *Ethical CS*

It draws on [Lauren F. Klein](https://lklein.com/)'s lab implementation of Peck's exercise, developed for the Spring 2020 Emory University course [QTM 490 "Feminist Data Science"](https://github.com/laurenfklein/feminist-data-science).
- [Jupyter notebook for lab activity](https://github.com/laurenfklein/feminist-data-science/blob/master/notebooks/lab1-hiring/Hiring-Filter-inclass.ipynb)

# Table of Contents

- [Scenario](#scenario)
- [Applicant Data](#applicant-data)
- [Objective](#objective)
- [Loading the Data](#loading-the-data)
- [Writing the Algorithm](#writing-the-algorithm)
- [Applicant Stories](#applicant-stories)
  * [Reflection Questions](#reflection-questions)
- [Lab Notebook Questions](#lab-notebook-questions)

# Scenario

Imagine you are working for *Moogle*, a well-known tech company that receives tens of thousands of job applications from graduating seniors every year.

Since the company receives too many job applications for HR to individually assess in a reasonable amount of time, you are asked to create a program that algorithmically analyzes applications and selects the ones most worth passing onto HR.

# Applicant Data

*Moogle* receives an overwhelming number of applications for open positions.

So the company has designed an application form that is designed to get numerical data from applicants.

This data is run through a screening algorithm to determine what applicants make the first-pass cut.

Job applications must enter the grades they received in 6 core Computer Science courses, as well as their overall GPA. 

For your convenience, this will be stored in a python `list` that you can access.

For example, a student who received the following scores...

- **Intro to CS:** 100
- **Data Structures:** 95
- **Software Engineering:** 80
- **Algorithms:** 89
- **Computer Organization:** 91
- **Operative Systems:** 75
- **Overall College GPA:** 83

... would result in the following list: `[100, 95, 80, 89, 91, 75, 83]`. 

You can assume that index `0` is *always* Intro to CS, `1` is *always* Data Structures, etc.

Because you are processing many applications, your program will receive a *list of lists*. 

For example, this would be the information for 3 applicants:

`[ 
    [100, 95, 80, 89, 91, 75, 83], 
    [75, 80, 85, 90, 85, 88, 90], 
    [85, 70, 99, 100, 81, 82, 91] 
 ]`

# Objective

Your task in this lab is to write a program that takes applicant data and automates the first-pass cut decision process.

The first step is to determine how you are going to select top applicants.

The underlying logic or criteria are the foundation for the Python program.

The second step is to write a Python function or program that will return first-pass candidates based on a desired set of critera.

# Loading the Data

We'll be working with two datasets for this task.

The first is `example_list`, which contains sample data for a limited number of applicants.

We can load that data manually.

```Python
example_list = [[93, 89, 63, 88, 60, 73, 80], [100, 63, 57, 96, 58, 71, 78], [81, 91, 99, 78, 57, 87, 86], [81, 73, 100, 57, 91, 60, 66], [86, 89, 64, 81, 69, 93, 92], [78, 63, 88, 95, 59, 98, 90], [55, 74, 68, 55, 69, 94, 80], [64, 77, 75, 92, 77, 72, 83], [95, 58, 92, 62, 77, 64, 59], [94, 78, 84, 83, 68, 63, 76]]

example_list
```

The second dataset `allApps` contains randomly-generated data for 10,000 applicants.

This data is stored in the `allApps.py` file.

You'll need to save and load this file in your local Python environment.

```Python
# instructions for a Jupyter notebook
%load allApps.py

# check loaded data
allApps
```

```Python
# instructions for Spyder or other non-notebook IDE
from allApps import allApps

# check loaded data
allApps
```

We'll come back to this data later.

# Writing the Algorithm

Remember the format of each app:

`[0]` - Intro to CS: 100

`[1]` - Data Structures: 95

`[2]` - Software Engineering: 80

`[3]` - Algorithms: 89

`[4]` - Computer Organization: 91

`[5]` - Operative Systems: 75

`[6]` - Overall College GPA: 83


We can use the `example_list` to start with building this program.

Let's say one of your criteria is a minimum overall college GPA of 80.

We can write a program that uses a `for` loop, tests for the GPA field value condition, and returns only list entries that meet the condition.

```Python
# create list to hold candidates who make it through first-pass cuts
finalists = list()

# for loop that takes example list, tests for GPA value
for app in example_list: # iterates through each applicant in example_list
  if app[6] > 80: # looks at the seventh field, overall GPA
    finalists += [app] # adds applicants that meet this condition to the finalists lists
    
# show list of applicants that made it through first-pass cuts
finalists
```

We can see from the output that, based on this criteria, four applicants would make it past the first-pass cuts.

Another example, this time with the criteria that applicants have no grade below 65.

```Python
# create list to hold candidates who make it through first-pass cuts
finalists = list()

# for loop that takes example list, tests for GPA value
for app in example_list: # iterates through each applicant in example_list
  if app[0] > 65 and app[1] > 65 and app[2] > 65 and app[3] > 65 and app[4] > 65 and app[5] > 65: # looks at all fields and only executes next line if all conditions are met
    finalists += [app] # adds applicants that meet this condition to the finalists lists
    
# show list of applicants that made it through first-pass cuts
finalists
```

A couple sample criteria that might get you started as you write this program.
- Applicants that have at least 4 grades above 85
- Applicants that have an average grade above 85

<blockquote>QX: Work together to determine the cutoff points or critera for the first-pass cuts. List your criteria and describe the decision making process used to arrive at those criteria.</blockquote>

<blockquote>QX: Include code + comments for a Python program that implements your criteria.</blockquote>

Once you have a working program using the `example_list` data, run the program on the `allApps` data.

<blockquote>QX: Roughly what percentage of applicants make it through the first-pass cuts? What are your thoughts on the effectiveness or efficacy of your algorithm? What would be your next step in continuing to develop or refine this algorithm?</blockquote>

Code that can help you determine percentage of applicants that make it through first-pass cuts.
```Python
for finalist in finalists:
    print(finalist)
print("Your algorithm kept", round(len(finalists)/len(allApps)*100), "percent of applicants")
```
    
# Applicant Stories

Now that you've developed a working algorithm, let's think through how your algorithm would handle some specific applicant use cases.

## Story 1

How would your algorithm handle an excellent candidate who thought they should put in letter grades?
`[‘A’, ‘A’, ‘A’, ‘A’, ‘A’, ‘A’, ‘A’]`

Or a candidate who entered their grades on a 4-point scale?
`[4, 3.9, 4, 4, 3.95, 4, 3.9]`

## Story 2

How would your algorithm handle a candidate that tested out of or didn't take *Intro to Computer Science*.

Or let's say this candidate saw the form and thought putting `-1` in that field would make it clear they did not take the course.
`[-1, 95, 99, 94, 96, 98, 95]`

## Story 3

How would your algorithm handle an applicant who mistyped one of input data points?

Maybe they accidentally added or inflated a number.
`[681, 68, 73, 70, 81, 91, 59]`

Or maybe they dropped a number.
`[100, 100, 100, 100, 100, 100, 10]`

## Story 4

How would your algorithm handle an applicant who had a medical emergency or personal tragedy one semester?
`[95, 93, 50, 91, 98, 90, 90]`

## Story 5

How would your algorithm handle an applicant who came from an underresourced background?

This applicant struggled at the beginning of college in their early courses but showed extraordinary growth by the time they graduated.
`[65, 75, 85, 95, 100, 100, 80]`

Or an inverse trajectory- a candidate who performed well in early courses but then coasted through later coursework.
`[100, 100, 95, 85, 75, 65, 80]`

How would your algorithm treat each of these candidates?

## Reflection Questions

These stories highlight the necessity of critically reflecting on the decisions made when building an algorithm, as well as possible tradeoffs.

<blockquote>QX: What systemic advantages/disadvantages are your algorithms likely to amplify?</blockquote>

<blockquote>QX: What does it mean to design a fair algorithm?</blockquote>

<blockquote>QX: What is the human cost of efficiency? More permissive algorithms may capture more interesting candidates, but it also means more costly, human work. What would an ideal balance look like?</blockquote>

# Hiring Algorithms in the Real World

To learn more about real-world applications of the type of system we developed in this lab:
- David Gershgorn, "[Companies are on the hook if their hiring algorithms are biased](https://qz.com/1427621/companies-are-on-the-hook-if-their-hiring-algorithms-are-biased/)" *Quartz* (22 October 2018)
- Rachel Kraus, "[Amazon used AI to promote diversity. Too bad it's plagued with gender bias.](https://mashable.com/article/amazon-sexist-recruiting-algorithm-gender-bias-ai/)" *Mashable* (10 October 2018)
- Gideon Mann and Cathy O'Neil, "[Hiring Algorithms Are Not Neutral](https://hbr.org/2016/12/hiring-algorithms-are-not-neutral)" *Harvard Business Review* (9 December 2016)
- Claire Cain Miller, "[Can an Algorithm Hire Better Than a Human?](https://www.nytimes.com/2015/06/26/upshot/can-an-algorithm-hire-better-than-a-human.html)" *New York Times* (25 June 2015)
- Aarti Shahani, "[Now Algorithms Are Deciding Whom To Hire, Based on Voice](https://www.npr.org/sections/alltechconsidered/2015/03/23/394827451/now-algorithms-are-deciding-whom-to-hire-based-on-voice)" *All Tech Considered* segment heard on NPR's *All Things Considered* (23 March 2015)
- Jeffrey Dastin, "[Amazon scraps secret AI recruiting tool that showed bias against women](https://www.reuters.com/article/us-amazon-com-jobs-automation-insight/amazon-scraps-secret-ai-recruiting-tool-that-showed-bias-against-women-idUSKCN1MK08G)" *Reuters* (10 October 2018)

# Lab Notebook Questions
