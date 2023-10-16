<script>
    import { onMount } from 'svelte';
    import { Chart, BarSeries, Category, DataLabel } from '@syncfusion/ej2-charts';
    Chart.Inject(BarSeries, Category, DataLabel);

    let chartData = []; // Initialize with an empty array

    function getRandomColor() {
        const letters = "0123456789ABCDEF";
        let color = "#";
        for (let i = 0; i < 6; i++) {
            color += letters[Math.floor(Math.random() * 16)];
        }
		console.log(color)
        return color;
    }



    onMount(async () => {
        // Fetch data from the API
        const apiUrl = 'https://api.recruitly.io/api/dashboard/ats/data/rejectreasons?start=01%2F01%2F2023&end=11%2F10%2F2023&apiKey=TEST45684CB2A93F41FC40869DC739BD4D126D77';

        try {
            const response = await fetch(apiUrl);
            if (response.ok) {
                const jsonData = await response.json();
                // Transform API data into the format suitable for the chart
                chartData = jsonData.slice(0, 6).map((item, index) => ({
                x: item.reason || 'Unknown',
                y: item.count,
                fill: getRandomColor(), // Generate a random color for each data point
            }));
                // Sort the chart data by y value
                chartData.sort((a, b) => a.y - b.y);

                // Refresh the chart with the updated data
                updateChart();
            } else {
                console.error('Failed to fetch data from the API.');
            }
        } catch (error) {
            console.error('An error occurred while fetching data:', error);
        }
    });

    // Function to create or update the chart
    function updateChart() {
		const data = chartData.map(item => ({ ...item, fill: getRandomColor() }));
        // Create and append the chart with the updated data source
        const chart = new Chart({
            primaryXAxis: {
                valueType: 'Category',
                majorGridLines: { width: 0 },
                labelStyle: {
                    size: '1rem',
                 fontWeight:"510",
                 fontFamily: 'sans-serif',
        
        },
              
            },
            primaryYAxis: {
                majorTickLines: { width: 0 },
                minorTickLines: { width: 0 },
                lineStyle: { width: 0 },
                labelStyle: {
                    size: '1rem',
                 fontWeight:"400",
                 fontFamily: 'sans-serif'
         
        
        },
            },
            width: '1350px',
            height: "390px",
          
            series: [
                {
                    type: 'Bar',
                    dataSource: chartData,
                    xName: 'x',
                    width: 2,
                    yName: 'y',
					fill:getRandomColor(),
                    columnSpacing: 0.1,
                    animation: {
                        enable: true,
                        duration: 1000,
                        delay: 200
                    },
                    cornerRadius: {
                        topRight: 5,
                        bottomRight: 5
                    },
                    marker: {
                        dataLabel: {
                            visible: true,
                            position: "Bottom",
                            font: {
                                fontWeight: 'bold',
                                color: 'white',
                                size: '17px'
                            }
                        }
                    },
					
                },
            ],
            
        });

        chart.appendTo('#container');
    }
</script>


        <div id='container'></div>


        <style>
            #container {
                margin-top: 40px; /* Add top margin */
                margin-bottom: 20px; /* Add bottom margin */
            }
        </style>
