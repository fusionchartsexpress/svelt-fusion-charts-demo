<script>
// General imports for all fusion charts
import FusionCharts from "fusioncharts";
import FusionTheme from "fusioncharts/themes/fusioncharts.theme.fusion";

// Required for charts
import Charts from "fusioncharts/fusioncharts.charts";

// Required for gauges
import Widgets from "fusioncharts/fusioncharts.widgets";

// Required for maps
import Maps from "fusioncharts/fusioncharts.maps";
import World from "fusioncharts/maps/fusioncharts.world";

// Required for all types
import SvelteFC, { fcRoot } from "svelte-fusioncharts";

// FusionCharts should always be first parameter. You can omit 
// what is not required
fcRoot(FusionCharts, Charts, Maps, World, Widgets, FusionTheme);

// Add data of continents from www.enchantedlearning.com
// Needed for map and chart
const continentData = [
    {
      id: "NA",
      label: "North America",
      value: "16.3",
      showLabel: "1"

    },
    {
      id: "SA",
      label: "South America",
      value: "12.0",
      showLabel: "1"
    },
    {
      id: "AS",
      label: "Asia",
      value: "30.0",
      showLabel: "1"
    },
    {
      id: "EU",
      label: "Europe",
      value: "6.7",
      showLabel: "1"
    },
    {
      id: "AF",
      label: "Africa",
      value: "20.3",
      showLabel: "1"
    },
    {
      id: "AU",
      label: "Australia",
      value: "5.2",
      showLabel: "1"
    }
  ];

  // For captions and subcaptions
const caption = "Percentage of Land Area on Planet Earth";
const subcaption = "Data Source: www.enchantedlearning.com";

// Add color ranges for map and guage
const colorRange = {
    minvalue: "0",
    code: "#87CEFA",
    gradient: "1", 
    color: [
      {
        minvalue: "0.0",
        maxvalue: "5.0",
        color: "#87CEFA"
      },
      {
        minvalue: "5.0",
        maxvalue: "10.0",
        color: "#87CEEB"
      },
      {
        minvalue: "10.0",
        maxvalue: "25.0",
        color: "#00BFFF"
      },      
      {
        minvalue: "25.0",
        maxvalue: "100.0",
        color: "#0000FF"
      }
    ]
};

// Add chart configuration
const chartConfigs = {
    type: "column2d", 
    height: 400, 
    width: 600, 
    dataFormat: "json", 
    renderAt: "chart-container", 
    dataSource: {
      chart: {
       caption: caption,
       subCaption: subcaption,
       xAxisName: "Continent", 
       yAxisName: "% Land Area", 
       numberSuffix: "%",
       theme: "fusion"   
      },
      //Include chartData from STEP 2
      data: continentData
    }
  }; 

// Add gauge configuration
const guageConfigs = {
    type: "angulargauge", 
    width: "450", 
    height: "300",
    dataFormat: "json", 
    renderAt: "guage-container", 
    dataSource: {
     chart: {
      caption: "Percentage Land Area of Asia",
      lowerLimit: "0",
      upperLimit: "100",
      showValue: "1",
      numberSuffix: "%",
      theme: "fusion"
    },
    // Chart Data
    colorRange: colorRange,
    dials: {dial: [{value: "30"} ]}
  }
};

// Add map configuration
const mapConfigs = {
    type: "world", // Map type
    width: "600", // Width of the chart
    height: "400", // Height of the chart
    dataFormat: "json", // Data Type
    renderAt: "map-container", 
    dataSource: {
      // Map Configuration
      chart: {
        caption: caption,
        subcaption: subcaption,
        numbersuffix: "%",
        includevalueinlabels: "1",
        labelsepchar: " - ",
        entityFillHoverColor: "#FFF9C4",
        theme: "fusion"
      },
      colorrange: colorRange,
      data: continentData
    }
  };

</script> 

<SvelteFC {...chartConfigs}/> 
<SvelteFC {...guageConfigs}/> 
<SvelteFC {...mapConfigs} />






