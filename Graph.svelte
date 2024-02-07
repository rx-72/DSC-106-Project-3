<script>
    import * as d3 from 'd3';

    // grabbing the data
    export let data;

    //setting dimensions
    const width = 928;
    const height = 600;
    const marginTop = 20;
    const marginRight = 30;
    const marginBottom = 30;
    const marginLeft = 40;

    // create x and y axis scales
    $: x = d3.scaleUtc()
    .domain(d3.extent(data, (d) => d.year))
    .range([marginLeft, width - marginRight]);

    $: y = d3.scaleLinear()
    .domain(d3.extent(data, (d) => d.solar_electricity)).nice()
    .range([height - marginBottom, marginTop]);

    //creating svg image
    const svg = d3.create("svg")
        .attr("width", width)
        .attr("height", height)
        .attr("viewbox", [0, 0, width, height])
        .attr("style", "max-width: 100%; height: auto; overflow: visible; font: 10px sans-serif;)

    //creating line connection data points
    $: const line = d3.line();
    $: path = svg.append("g")
        .attr("fill", "none")
        .attr("stroke", "steelblue")
        .attr("stroke-width", 1.5)
        .attr("stroke-linejoin", "round")
        .attr("stroke-linecap", "round")
    .selectAll("path")
    .data(groups.values())
    .join("path")
        .style("mix-blend-mode", "multiply")
        .attr("d", line);

</script>