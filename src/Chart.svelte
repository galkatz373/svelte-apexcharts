<script>
  import { onMount, onDestroy } from 'svelte';
  let chartNode, chart;
  export let options;

  onMount(async () => {
    const ApexCharts = (await import('apexcharts')).default;

    chart = new ApexCharts(chartNode, options);
    chart.render();
  });

  $: if (chart && options) chart.updateOptions(options);

  onDestroy(() => {
    if (chart) chart.destroy();
  });
</script>

<div bind:this={chartNode} />
