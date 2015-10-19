# Superfly Financial data protoype
A quick protoype showing a financial dashboard for use either in house or as a sales tool for financial customers. 

The idea is to showcase linked charts, which together allow a quick understanding of the data and the ability to break it down into smaller segments, to see how each one influences the overall picture.  

To use simply clone the repository locally and serve with 
```bash
python -m SimpleHTTPServer 
```
#Highlights
I used [dc.js](http://dc-js.github.io/dc.js/examples/filtering.html) to build this, which focuses on the idea of dimensions and groups.  Their is an intial chunk of code
```javascript

var ndx = crossfilter(spendData),
        yearDim  = ndx.dimension(function(d) {return +d.year;}),
        spendDim = ndx.dimension(function(d) {return Math.floor(d.total_usd/10);}),
        nameDim  = ndx.dimension(function(d) {return d.brand_name;}),
        dateDim = ndx.dimension(function(d) {return d.date;}),
        monthDim = ndx.dimension(function(d) {return d.date.getMonth();}),
```
Which defines the different dimensions by which to slice the data. 
Then we proceed to create "Groups", which takes each point in that dimension and "groups together" all the data with a particular value, caclculating an aggreagte result for it. Its easier with an example
````javascript
spendPerYear = yearDim.group().reduceSum(function(d) {return Math.abs(+d.total_usd);})
````
This line  groups together all the data for each year, and returns the sum of all of the total_usd fields in it. 

