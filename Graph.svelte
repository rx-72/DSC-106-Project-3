<script>
    import * as d3 from 'd3';

    // grabbing the data
    export let data;
    let svg;

    // Placeholders for the axis elements.
    let gx;
    let gy;

    $: console.log(data)

    //setting dimensions
    const width = 928;
    const height = 600;
    const marginTop = 20;
    const marginRight = 30;
    const marginBottom = 30;
    const marginLeft = 40;

    // create x and y axis scales
    $: x = d3
    .scaleUtc()
    .domain(d3.extent(data, (d) => d.year))
    .range([marginLeft, width - marginRight]);

    $: y = d3.scaleLinear()
    .domain(d3.extent(data, (d) => d.electricity_generated)).nice()
    .range([height - marginBottom, marginTop]);

    $: d3.select(gx).call(d3.axisBottom(x).ticks(width / 80));
    $: d3.select(gy)
    .call(d3.axisLeft(y).ticks(null, '+'))
    // grid lines
    .call((g) =>
      g
        .selectAll('.tick line')
        .clone()
        .attr('x2', width - marginRight - marginLeft)
        .attr('stroke-opacity', (d) => (d === 0 ? 1 : 0.1)),
    );

</script>

    <div class="coal-coal_electricity generation">
        <svg
            {width}
            {height}
            viewBox="0 0 {width} {height}"
            style="max-width: 100%; height: auto; overflow: visible; font: 10px sans-serif;"
        >

            <!-- x-axis -->
            <g bind:this={gx} transform="translate(0,{height - marginBottom})" />
            <!-- y-axis -->
            <g bind:this={gy} transform="translate({marginLeft},0)">
            <text
                x="5"
                y={marginTop}
                dy="0.32em"
                fill="#000"
                font-weight="bold"
                text-anchor="start"
            >
                Electricity generated per year (Terawatt-hours)
            </text>
        </g>

        </svg>
    </div>