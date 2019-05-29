# CARTO VL Cluster Workshop

## Introduction

This is the content for the CARTO VL Webinar "Discover the Power of CARTO VL for Visual and Interactive Analysis". Through these seven steps, you'll understand how cluster aggregation works and how to create an interactive map.

<video width="600" height="400" controls>
  <source src="/steps/video/final-map.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>

## Data

We're using a dataset based on the [Police Department Incident Reports](https://data.sfgov.org/Public-Safety/Police-Department-Incident-Reports-2018-to-Present/wg3w-h783) of San Francisco for 2019. They have a great [map visualization](https://data.sfgov.org/Public-Safety/Map-of-Police-Department-Incident-Reports-2018-to-/jq29-s5wp). You can take a look to it in order to understand the data we're going to be working with.

## Workshop Steps

### 1. Create the basic structure from an example

* [CARTO VL examples](https://carto.com/developers/carto-vl/examples/)
* [Source](step-1.html)

![Step 1 - Basic CARTO VL map](/steps/img/step-1.png)

### 2. Add your credentials and change settings

* [Getting Started Guide](https://carto.com/developers/carto-vl/guides/getting-started/)
* [Source](step-2.html)

Notes:

* For this visualization, we have decided to use the `darkmatter` basemap.
* You can get the center and the zoom of your map by going to the console and accessing the `map` object.

![Step 2 - Change settings](/steps/img/step-2.png)

### 3. Style by using cluster count

* [clusterCount Expression](https://carto.com/developers/carto-vl/reference/#cartoexpressionsclustercount)
* [Source](step-3.html)

Notes:

* We use `sqrt(@cluster_count)` in order to decrease each feature size proportionally.
* Try change the resolution value and see what happens.
* Let's change the styles: remove the stroke, change the color, add opacity.

![Step 3 - Style by cluster count](/steps/img/step-3.png)

### 4. Add labels using Mapbox

* [Points labels CARTO VL example](https://carto.com/developers/carto-vl/examples/#example-point-labels)
* [Label Cluster Count](https://carto.com/developers/carto-vl/examples/#example-label-cluster-counts)
* [Mapbox label documentation](https://docs.mapbox.com/mapbox-gl-js/example/display-and-style-rich-text-labels/)
* [Source](step-4.html)

![Step 4 - Add labels using Mapbox](/steps/img/step-4.png)

Notes:

* First, let's use the viewport features expression to get the cluster count of each cluster feature present in the viewport.
* Second, copy the code from the Label Cluster Count example above to set up the labels layer when the layer is loaded.
* Understand the how the filter style property works.
* Zoom in and zoom out to see the changes.

### 5. Use clusterMode expression to color the clusters

* [clusterMode expression](https://carto.com/developers/carto-vl/reference/#cartoexpressionsclustermode)

Notes:

* If we would like to change the width depending on the `$incident_category` column instead of the cluster count, we'd have to use it along with `clusterMode` because it has been already aggregated.
* Filter labels: difference between `string` and `number`

![Step 5 - Use clusterMode to color the clusters](/steps/img/step-5.png)

### 6. Visualize incidents by day using an interactive based filter

* [Interactive based filter CARTO VL example](https://carto.com/developers/carto-vl/examples/#example-interactive-based-filter)

Notes:

* We're coloring now the clusters based on the `$incident_day_of_week` column (from 'Monday' to 'Sunday')
* To improve the visualization style, we're adding a border to the features with the stroke style properties.
* Let's use `buckets` in the color ramp to sort the legend by day of the week, which is saved in the `days` array.

```html
<section>
  <div id="controls">
    <ul id="content"></ul>
  </div>
</section>
```

![Step 6 - Add an interactive based filter](/steps/img/step-6.png)

### 7. Use a dropdown to filter by categories

Notes:

* We set an initial filter of 0 in the viz style to avoid a flickering effect when updating the map at the beginning
* We're adding a new method `generateSelectors` that we're using after `generateLegend`.
* We're also adding `updateFilter` method to reuse it.

```html
<ul class="dataview">
  <li>
    <label class="label"><p>Incident Category<p></label>
    <select id="js-incident-selector" class="select"></select>
  </li>
</ul>
```

![Step 7 - Add a dropdown selector](/steps/img/step-7.png)