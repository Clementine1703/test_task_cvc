<template>
	<div>
		<Pie :data="chartdata"/>
	</div>
	<!-- <Bar :data="chartData" /> -->


</template>
  
<script>
import {
	// Bar,
	Pie,
} from 'vue-chartjs'
import { Chart as ChartJS, ArcElement, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js'

ChartJS.register(Title, ArcElement, Tooltip, Legend, BarElement, CategoryScale, LinearScale)

export default {
	name: 'PieChart',
	props: [
		'chartdata',
	],
	components: {
		// Bar,
		Pie,
	},
	data() {
		return {
			chartData1: {
				labels: ['VueJs', 'EmberJs', 'ReactJs', 'AngularJs'],
				datasets: [
					{
						backgroundColor: ['#41B883', '#E46651', '#00D8FF', '#DD1B16', 'rgba(255,99,132,1)', 'rgba(54, 162, 235, 1)', 'rgba(255, 206, 86, 1)', 'rgba(75, 192, 192, 1)'],
						data: [40, 20, 80, 10]
					}
				]
			},
			// chartData: {
			// 	labels: [
			// 		'Red',
			// 		'Blue',
			// 		'Yellow'
			// 	],
			// 	datasets: [{
			// 		label: 'My First Dataset',
			// 		data: [300, 50, 100],
			// 		backgroundColor: [
			// 			'rgb(255, 99, 132)',
			// 			'rgb(54, 162, 235)',
			// 			'rgb(255, 205, 86)'
			// 		],
			// 		hoverOffset: 4
			// 	}]
			// },
		}
	},
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
div {
	width: 200px;
	background-color: white;
	border-radius: 10px;
}
</style>