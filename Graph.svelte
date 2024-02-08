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
    const marginTop = 10;
    const marginRight = 30;
    const marginBottom = 20;
    const marginLeft = 100;

    // create x and y axis scales
    $: x = d3
    .scaleUtc()
    .domain(d3.extent(data, (d) => d.year))
    .range([marginLeft, width - marginRight]);

    $: y = d3.scaleLinear()
    .domain([0, 11000]).nice()
    .range([height - marginBottom, marginTop])

    $: d3.select(gx).call(d3.axisBottom(x).ticks(width / 80));
    $: d3.select(gy)
    .call(d3.axisLeft(y).ticks())
    // grid lines
    .call((g) =>
      g
        .selectAll('.tick line')
        .clone()
        .attr('x2', width - marginRight - marginLeft)
        .attr('stroke-opacity', (d) => (d === 0 ? 1 : 0.1)),
    );

    $: countries = d3.group(data, d => d.country);
    $: console.log(countries)

    $: color = d3
    .scaleOrdinal()
    .domain(countries)
    .range(["#3957ff", "#d3fe14", "#c9080a", "#fec7f8", "#0b7b3e", "#0bf0e9", 
    "#c203c8", "#fd9b39", "#888593", "#906407", "#98ba7f", "#fe6794", 
    "#10b0ff", "#ac7bff", "#fee7c0", "#964c63", "#1da49c", "#0ad811", 
    "#bbd9fd", "#fe6cfe", "#297192", "#d1a09c", "#78579e", "#81ffad", 
    "#739400", "#ca6949", "#d9bf01", "#646a58", "#d5097e", "#bb73a9", 
    "#ccf6e9", "#9cb4b6", "#b6a7d4", "#9e8c62", "#6e83c8", "#01af64", 
    "#a71afd", "#cfe589", "#d4ccd1", "#fd4109", "#bf8f0e", "#2f786e", 
    "#4ed1a5", "#d8bb7d", "#a54509", "#6a9276", "#a4777a", "#fc12c9", 
    "#606f15", "#3cc4d9", "#f31c4e", "#73616f", "#f097c6", "#fc8772", 
    "#92a6fe", "#875b44", "#699ab3", "#94bc19", "#7d5bf0", "#d24dfe", 
    "#c85b74", "#68ff57", "#b62347", "#994b91", "#646b8c", "#977ab4", 
    "#d694fd", "#c4d5b5", "#fdc4bd", "#1cae05", "#7bd972", "#e9700a", 
    "#d08f5d", "#8bb9e1", "#fde945", "#a29d98", "#1682fb", "#9ad9e0", 
    "#d6cafe", "#8d8328", "#b091a7", "#647579", "#1f8d11", "#e7eafd", 
    "#b9660b", "#a4a644", "#fec24c", "#b1168c", "#188cc1", "#7ab297", 
    "#4468ae", "#c949a6", "#d48295", "#eb6dc2", "#d5b0cb", "#ff9ffb", 
    "#fdb082", "#af4d44", "#a759c4", "#a9e03a", "#0d906b", "#9ee3bd", 
    "#5b8846", "#0d8995", "#f25c58", "#70ae4f", "#847f74", "#9094bb", 
    "#ffe2f1", "#a67149", "#936c8e", "#d04907", "#c3b8a6"])
    $: console.log(color)

    $: line = d3.line();



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
        <path
            fill="none"
            stroke={color(data.country)}
            stroke-width=1.5
            stroke-linejoin="round"
            stroke-linecap="round"
            d=line
        >
            
        </path>

        <!-- points -->
        <g stroke="#000" stroke-opacity="0.2">
            {#each data as d, i}
                <circle
                key={i}
                cx={x(d.year)}
                cy={y(d.electricity_generated)}
                fill={color(d.country)}
                r="2.5"
                />
            {/each}
        </g>

        </svg>
    </div>