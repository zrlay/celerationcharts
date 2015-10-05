
## Celeration Charts


> The Standard Celeration Chart (SCC) is more than a mere data-display tool; it guides its user to make data-driven
analytical decisions. It represents data proportionally and multiplicatively – how it changes in the natural environment.
Further, the chart allows us to predict future performance by the use of the straight Celeration Line.
>
> The SCC was developed in 1967 by “Ogden Lindsley, Eric Haughton, (and several other graduate students of Lindsley’s),
Sandy Houston (the administrative assistant), and Helen Brennan (the printer)” (Potts, Eshleman, & Cooper, 1993).

\- [celeration.org](http://celeration.org/learning-area/the-standard-celeration-chart/)

The charts generated in this software package are intended to reflect the
critical attributes of the standard charts first developed by Dr. Ogden R. Lindsley.
The number of log-based cycles on the y-axis,
amount and distribution of calendar time intervals on the x-axis, number of celeration periods,
and aspect ratio are designed to be consistent with the attributes described by Dr. Lindsley.
No digital representation of the standard charts can entirely reproduce all of the standards maintained by the printed format.
We encourage anyone interested in using these charts in print to purchase copies from the Behavior Research Company.

The Standard Celeration Chart is copyright © 1998 Behavior Research Company http://www.behaviorresearchcompany.com/.

### Using the Charts

The charts in this package are extensions of Google charts, and use much of the google visualization API and chart
options.

You must load the AJAX API.
```
<script type="text/javascript" src="https://www.google.com/jsapi"></script>
```

Include the minified celeration chart file.
```
<script type="text/javascript" src="celerationchart.min.js"></script>
```

Load the Visualization API and instantiate the chart.
```
<script type="text/javascript">

    // Load the Visualization API and the base chart package.
    google.load('visualization', '1', {packages: ['corechart']});


    // Set a callback to run when the Google Visualization API is loaded.
    google.setOnLoadCallback(drawChart);


    // Callback that creates and populates a data table,
    // instantiates the celeration chart, passes in the data and
    // draws it.
    function drawChart() {

        // Create the data table.
        var data = new google.visualization.DataTable();

        // Set any additional chart options. Style and axes options specific to the celeration chart will not get
        overriden.
        options = {};

        // Instantiate with chart height and draw the chart, passing in data and options.
        var programmaticChart = new CelerationChart(document.getElementById('programmatic_chart_div'), 600);
        programmaticChart.draw(data, options)
    }

</script>
```

When instantiating a CelerationChart, you **must** provide the chart `height` in addition to the `DOM element` in which
 the chart will be drawn in order for the chart to maintain the aspect ratio of the standard chart.

### Loading existing data

Please refer to the [DataTable section in the Google Charts documentation](https://developers.google
.com/chart/interactive/docs/datatables_dataviews).

#### What Table Schema Does My Chart Use?
The celeration chart acts as a scatter chart. For a single series chart, each row is a point, and the two columns are
 the X and Y values.
 For a chart with multiple series, such as one series for corrects and one for errors, each row is a point and the
 first column is its X value, the second column is the 'Corrects series' Y-Value (Series 0), the third column is the
 'Errors
 series' Y-Value  (Series 1).

 You can specify any style options you want for each series. Any series style not specified will default to a
 'circle' point shape.

 You can change an error series to the typical "X" point mark like this:
 ```
 options = {
     series: {
         1: {
             pointShape: {
                 type: 'star',
                 sides: 4,
                 inset: 0.1,
                 rotation: 45
             },
             pointSize: 4
         }
     }
 };
 ```

[View example code.](index.html)

[Preview example page.](https://htmlpreview.github.io/?https://github.com/mightbejosh/celerationcharts/blob/master/index.html)

### Loading data from a Google Spreadsheet
This chart can accept a remote data source, such as a google spreadsheet.

```
function drawChart() {
    // Query the data from a remote Google Sheet.
    var query = new google.visualization.Query(
            'https://docs.google.com/spreadsheets/d/16-HQLHBJxGLXAgKQWIxq-9Z5dq51fQ1SnBLTBRpRTfQ/gviz/tq?gid=0&headers=1');
    query.send(handleQueryResponse);
}


function handleQueryResponse(response) {
    if (response.isError()) {
        alert('Error in query: ' + response.getMessage() + ' ' + response.getDetailedMessage());
        return;
    }

    // Create a data table from the remote spreadsheet.
    var data = response.getDataTable();

    // Set chart options
    options = {
        hAxis: {format: '#'},
        legend: {position: 'none'},
    };

    // Instantiate and draw our chart, passing in options.
    programmaticChart = new CelerationChart(document.getElementById('programmatic_chart_div'), 600);
    programmaticChart.draw(data, options);
}
```

[View example code.](linked-sheet-example.html)

[Preview example page.](https://htmlpreview.github.io/?https://github.com/mightbejosh/celerationcharts/blob/master/linked-sheet-example.html)


Please see (https://developers.google.com/chart/interactive/docs/spreadsheets) for more information.



### Events, and other methods
The Celeration chart is a simple wrapper around the google ChartWrapper that overrides various display and data
settings to closely imitate the standard celeration chart.

You can use all of the Google Visualization API, and ScatterChart, events and methods.

To access the ChartWrapper:
```
  chart = new CelerationChart(id, height)
  wrapper = chart.chartWrapper
```

To access the chart:
```
  chartInstance = wrapper.getChart()
```


### Convenience methods

Some convenience methods are available on the wrapper, which may be useful for typical celeration chart usage.

##### Trendlines
Turn on trendlines for any number of series:
```
  chart.setTrendlines([0,1,2])
```
Turn on trendlines for all series:
```
  chart.setTrendlines()
```
Turn off all trendlines:
```
  chart.removeTrendlines()
```

