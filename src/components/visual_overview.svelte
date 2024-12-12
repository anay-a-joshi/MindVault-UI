<script>
    /*
     * Name: Anay Abhijit Joshi
     * CS 5167: User Interface 1
     * Level: Undergraduate Student
    */

    import { onMount, afterUpdate } from "svelte";
    import Chart from "chart.js/auto";

    export let productivityData = [];
    export let categories = ['Learning/Practice Time', 'Stretching/Yoga Duration', 'Hydration Levels'];

    let doughnutCanvas;
    let barCanvas;

    let doughnutChartInstance = null;
    let barChartInstance = null;

    const renderDoughnutChart = () => {
        if (doughnutChartInstance) {
            doughnutChartInstance.destroy();
        }

        doughnutChartInstance = new Chart(doughnutCanvas, {
            type: 'doughnut',
            data: {
                labels: categories,
                datasets: [{
                    data: productivityData,
                    backgroundColor: ['#FF6347', '#457B9D', '#1D3557'],
                    hoverBackgroundColor: ['#FF7F50', '#589ACD', '#294E74'],
                    hoverOffset: 6
                }]
            },
            options: {
                plugins: {
                    legend: {
                        display: false // Hide legend
                    }
                }
            }
        });
    };

    const renderBarChart = () => {
        if (barChartInstance) {
            barChartInstance.destroy();
        }

        barChartInstance = new Chart(barCanvas, {
            type: 'bar',
            data: {
                labels: categories,
                datasets: [{
                    label: 'Productivity Metrics',
                    data: productivityData,
                    backgroundColor: ['#FF6347', '#457B9D', '#1D3557'],
                    borderColor: ['#E5533F', '#3D6989', '#162D49'],
                    borderWidth: 1
                }]
            },
            options: {
                plugins: {
                    legend: {
                        display: false
                    },
                    tooltip: {
                        callbacks: {
                            label: function (tooltipItem) {
                                return `${tooltipItem.raw} units`;
                            }
                        }
                    }
                },
                scales: {
                    x: {
                        ticks: {
                            color: '#1D3557',
                            font: {
                                size: 12,
                                weight: 'bold'
                            }
                        }
                    },
                    y: {
                        ticks: {
                            color: '#1D3557',
                            font: {
                                size: 12,
                                weight: 'bold'
                            }
                        }
                    }
                }
            }
        });
    };

    onMount(() => {
        renderDoughnutChart();
        renderBarChart();
    });

    afterUpdate(() => {
        renderDoughnutChart();
        renderBarChart();
    });
</script>

<div class="charts">
    <div class="doughnut-section">
        <canvas bind:this={doughnutCanvas}></canvas>
        <div class="doughnut-labels">
            {#each categories as category, i}
                <div class="label-item">
                    <span class="color-box" style="background-color: {['#FF6347', '#457B9D', '#1D3557'][i]}"></span>
                    <span>{category}</span>
                </div>
            {/each}
        </div>
    </div>
    <canvas bind:this={barCanvas}></canvas>
</div>

<style>
    .charts {
        display: flex;
        justify-content: space-between;
        align-items: flex-start;
        gap: 2rem;
        padding: 1rem 0;
    }

    canvas {
        max-width: 48%;
        max-height: 450px;
    }

    .doughnut-section {
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 300px; /* Fixed width to maintain proper sizing */
        height: 300px; /* Fixed height to maintain aspect ratio */
        border: 4px solid #FF6347;
        border-radius: 50%;
        padding: 0.5rem;
    }

    .doughnut-labels {
        margin-top: 1.5rem;
        display: flex;
        flex-direction: column;
        align-items: flex-start;
    }

    .label-item {
        display: flex;
        align-items: center;
        margin-bottom: 0.5rem;
        font-size: 1rem;
    }

    .color-box {
        width: 16px;
        height: 16px;
        margin-right: 8px;
        border-radius: 4px;
        display: inline-block;
    }

    .charts canvas:last-child {
        width: 100%; /* Bar chart takes the remaining space */
        max-height: 450px;
        border: 4px solid #1D3557;
        padding: 0.5rem;
        border-radius: 5px;
    }
</style>
