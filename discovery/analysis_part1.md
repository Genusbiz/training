
**_Øvingsopplegg er under arbeid_**

# Analysis Part One - Trips and visualization of data

### SESSION BY INSTRUCTOR: 
_The instructor will start of by giving you a brief introduction to the topic. The session will include how to create a new analysis, how to add and modify tiles and how to preview the analysis. After the lesson the participants will recreate the analysis made in class._

#### Agenda 

- How to create and preview analysis
- Tiles: create, scale, customize appearance (header, background, etc.)
	- Tiletypes
		- Data
		- Format 
- Set up tile with selections (to filter data)
- Ignore selection

## Create, edit and preview analysis

To create an analysis open Genus Apps Discovery Desktop and choose the portal _Discovery_. This is where both Datamarts and Analysis are available. In the Discovery-panel click on _Analysis_ and _New_. Remember to save. To reopen an analysis in edit mode, right click the analysis and choose _Edit_.  

To preview an analysis either: 

- double click on the saved analysis in Discovery Desktop
- in the analysis editor click on "Action". In the action dropdown there are two preview choices, one for Genus Desktop preview and one for internet browser preview.   

## Analysis from class

Try to recreate the analysis shown in class/analysis in the solution environment. These are the steps: 

### Total number of trips

1. In the Discovery-panel click _Analysis_ and create a new analysis. Remember to save.  

2. In the analysis edit mode, create a new tile.

3. Scale the tile to match the solution environment and give the tile a header.

4. Choose tile type _Measure_.
	
    a. In DATA - Value - choose a data source and aggregation. 
	
    b. In FORMAT - Body - change font size and colour.

5. Save and preview 

### Number of trips per weekday

1. Create a new tile. Scale tile and give it a header. 

2. Choose tile type _Lines_.

    a. In DATA - Horizontal category - choose a data source.

    b. In DATA - Values - choose line/vertical data source.

    c. In FORMAT - Legend - set a legend position.

    d. In FORMAT - Axes - Primary Value Axis - Change number format to zero decimals.

    e. In FORMAT - Values - change number format to zero decimals and change data series color. Also set data point label to _custom_ and write {value}. This will make the values of each datapoint visible. 

3. Save and preview. 

### Selections with dropdown

1. Create a new tile. Scale tile and give it a header. 

2. Choose a tile type _Dropdown_
	
    a. Create a dropdown and choose a data source. The data source will appear in the analysis and open for filtering the analysis. for 

    b. Create two additional dropdowns in the same dropdown tile.  

3. Save and preview. While previewing, do a selection in the dropdown. Notice how the numbers in the different tiles change as selections are made. 

## Extra work 

- Create a tile that shows _% trips per borough type_ 
- Create a tile that shows _total amount per payment type_
