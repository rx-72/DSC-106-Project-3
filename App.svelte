<script>
    import * as d3 from 'd3';
    import { onMount } from 'svelte';
    import Graph from './Graph.svelte';

    let data = [];

    onMount(async () => {
        const res = await fetch(
            '/coal_gener_nonnull_filtered_countries_log.csv',
        );
        const csv = await res.text();
        await d3.csvParse(csv, (d) => {
            data.push({
               year: new Date(Date.UTC(d["year"])),
               country: d["country"],
               electricity_generated: d["coal_electricity"], 
            });
        });
        data = data;
    });

    $: console.log(data)
</script>

<main>
    <Graph {data} />
</main>