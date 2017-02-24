--- 
layout: post
title: How to create Gantt charts in Excel
---

I absolutely love Gantt charts.Gantt charts are often an indespensable tool for project managers as they are incredibly useful to visualize project's deadline and breakdown structure. It is a shame that Excel does not provide Gantt charts out of the box, but with a bit of tinkering it is possible to create beautiful Gantt charts in Excel. 

## Setting up the data
On the first row, as header, you should have three columns: start date, duration in days, and end date.
All tasks should be listed in the first column

[EXAMPLE]

## Creating the chart

Click on an empty cell and insert a 2d stacked horizontal bar from Charts in the Insert tab

You should have an empty chart in front of you. From the Design tab, select Select Data. You will have in front of you a window called Select Data Source divided in two: for now, let's concentrate on the left portion ("Legend Entries (Series)"). Click add, and insert a name for the series in the first input (e.g. "Start date") and the starting date range. Repeat the same procedure for the duration. Note that the duration is expressed in days: if you are plotting months or years, use a days calculator like [this one](http://www.easysurf.cc/ndate2.htm).

You should now look at a graph that vaguely resembles a Gantt chart, even though we're not quite there yet.

[EXAMPLE]

Now it's time to edit the Horizontal (Category) Axis Labels, on the right parte of the Select Source Data window. Click edit and select all your tasks on the first column on the left of your spreadsheet.

You might notice that the labels on the horizontal axis are in the reversed order compared to the data. You can easily fix that by right clicking on the labels and selecting "Categories in reverse order" from the Format Axis menu.

Your chart has two colors: the default is blue and orange. Click on the blue line and from the Format tibe select Shape Fill > No Fill. Aah, now looks much more like a Gantt chart! There are still a few things we can do to make it look nicer.

[EXAMPLE]

## Some tweaks

**Removing spaces at the beginning and end**: Right now our chart has a lot of white space at the beginning and the end of our plotted data. 

To remove those, you should right click on the earliest starting date and select Format Cell. The number should be formatted as a date. Click on the 'General' category and note the number listed under 'Sample'. It should look something like "43040" (that's the number for 1 November 2017) and we will need it in a moment. Do the same thing for the last ending date of your project and note the number listed under "General".
Now right click on the dates in the chart and select Format Axis. In the first two fields under Axis Options, Bonds Minimum and Maximum, and insert the two numbers found under the General options in Format Cell, corresponding to your start and end date of the whole project.

[EXAMPLE]

**Changing the periodization**: Depending on your project, you might want to break down your projects in weeks, months, quarters or else. The second option in the Axis Options, Units Major, will allow to set the timeframe of your project, expressed in days. Insert 7 for a week, 30 for a month, 183 for quarterly and so on. Leave the Units minor option as is.

[EXAMPLE]


# Look and feel

[EXAMPLE]
The chart is now finished, but it may look a bit... well, dull. Two easy ways to spark it up  would be to change the default font from Calibri to somethign a little bit more exciting. There are a lot of well-designed free fonts you can choose from in websites such as [Google Fonts](https://fonts.google.com) and [Font Squirrel](https://www.fontsquirrel.com/). A particular favourite of mine is Fira Sans, designed for Mozilla, but anything that ranks as popular is usually a safe choice.

To change the color of the bar, you can simply click on the bars. If you click once you will change the color of all bars, clicking twice will enable you to set a different color for each bar. I would suggest not to use the default color schemes available in Excel - they are ugly and defintely overused - and possibly to avoid the default colors. A better choice would be to create a good looking palette using a service like [Coolors](https://coolors.co/), or using your branding colors from the More Fill Colors option.

[EXAMPLE]

The most design-savvy may want to give the final touches from a graphical software. The easiest way to convert an Excel chart into a picture - either raster or vector - is to copy the graph into PowerPoint. From there you can either save it as an image (a png, jpg or bmp, depending on your preference) or as an emf if you wish to have a vector file.

For example, I saved my chart in an emf file that I later imported in Inscape, an open-source vector graphics software, for the final tweaks. I added few more color options and few other tweaks and saved the final product. 

Done! Your beautiful, informative Gantt chart is now ready!
