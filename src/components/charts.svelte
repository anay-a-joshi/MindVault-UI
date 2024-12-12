<!-- <script>
  import { onMount, onDestroy } from 'svelte';
  import Chart from 'chart.js/auto';

  export let entries = [];

  let moodChart, energyChart;

  onMount(() => {
    const moodCtx = document.getElementById('moodChart').getContext('2d');
    const energyCtx = document.getElementById('energyChart').getContext('2d');

    const dates = entries.map(entry => entry.date.toDateString());
    const moods = entries.map(entry => entry.mood);
    const energyLevels = entries.map(entry => entry.energyLevel);

    moodChart = new Chart(moodCtx, {
      type: 'line',
      data: {
        labels: dates,
        datasets: [
          {
            label: 'Mood Over Time',
            data: moods,
            borderColor: 'rgba(75, 192, 192, 1)',
            backgroundColor: 'rgba(75, 192, 192, 0.2)',
          },
        ],
      },
    });

    energyChart = new Chart(energyCtx, {
      type: 'bar',
      data: {
        labels: dates,
        datasets: [
          {
            label: 'Energy Level',
            data: energyLevels,
            backgroundColor: 'rgba(153, 102, 255, 0.5)',
            borderColor: 'rgba(153, 102, 255, 1)',
          },
        ],
      },
    });
  });

  onDestroy(() => {
    if (moodChart) moodChart.destroy();
    if (energyChart) energyChart.destroy();
  });
</script> -->
