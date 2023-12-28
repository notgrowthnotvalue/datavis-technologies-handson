<script>
  import { scaleBand, scaleLinear } from 'd3-scale';
  import { axisBottom, axisLeft } from 'd3-axis';
  import { max } from 'd3-array';
  import { onMount } from 'svelte';
  
  // Dimensions
  const width = 600;
  const height = 300;
  const margin = { top: 10, right: 10, bottom: 30, left: 60 };
  const innerWidth = width - margin.left - margin.right;
  const innerHeight = height - margin.top - margin.bottom;
  
  // Array
  const data = [
    { service: "Netflix", viewers: 2.9 },
    { service: "Amazon Prime Video", viewers: 1.3 },
    { service: "Disney+", viewers: 2.1 },
    { service: "Hulu", viewers: 0.9 },
    { service: "Apple TV", viewers: 1.1 },
    { service: "Rakuten", viewers: 0.4 }
  ];

  // Scales
  const xScale = scaleBand()
    .domain(data.map(d => d.service))
    .range([0, innerWidth])
    .padding(0.1);

  const yScale = scaleLinear()
    .domain([0, max(data, d => d.viewers)])
    .range([innerHeight, 0]);

  // Axes
  const xAxis = axisBottom(xScale);
  const yAxis = axisLeft(yScale);

  let xAxisGroup;
  let yAxisGroup;

  onMount(() => {
    xAxisGroup.call(xAxis);
    yAxisGroup.call(yAxis);
  });

</script>

<svg viewbox="0 0 {width} {height}" style="max-width: {width}px">
  <g transform={`translate(${margin.left},${margin.top})`}>
    {#each data as datum}
      <rect
        x={xScale(datum.service)}
        y={yScale(datum.viewers)}
        width={xScale.bandwidth()}
        height={innerHeight - yScale(datum.viewers)}
        fill="steelblue" 
      />
    {/each}

    <!-- X Axis -->
    <g 
      transform={`translate(0,${innerHeight})`} 
      bind:this={xAxisGroup} 
    ></g>
    
    <!-- Y Axis -->
    <g bind:this={yAxisGroup}></g>
  </g>
</svg>