<template>
	<div class="wrapper">
		<div class="accordion-menu">
			<ul>
				<li>
					<h1>Группы</h1>
				</li>
				<li v-for="group in groups" :key="group.id">
					<group-item  :group="group" @openpopup="open_popup"></group-item>
				</li>
			</ul>
		</div>
		<modal-window :popup="popup" @closepopup="close_popup"></modal-window>
		<div class="diagram-container">
			<pie-chart v-if="chart_data.labels.length > 0" class="diagram" :chartdata="chart_data"></pie-chart>
		</div>
	</div>
</template>

<script>
import PieChart from './PieChart.vue'
import GroupItem from './GroupItem.vue'
import ModalWindow from './ModalWindow.vue'
const axios = require('axios')

export default {
	name: 'MyGroups',
	components: {
		PieChart,
		GroupItem,
		ModalWindow,
	},
	data() {
		return {
			groups: '',
			popup: {
				visible: false,
				description: '',
				title: '',
			},
			chart_data: {
				labels: [],
				datasets: [
					{
						backgroundColor: ['#41B883', '#E46651', '#00D8FF', '#DD1B16', 'rgba(255,99,132,1)', 'rgba(54, 162, 235, 1)', 'rgba(255, 206, 86, 1)', 'rgba(75, 192, 192, 1)'],
						data: []
					}
				]
			}
		}
	},
	mounted() {
		this.get_a_list_of_groups()

	},
	methods: {
		get_a_list_of_groups() {
			var config = {
				method: 'get',
				url: `http://62.217.182.170/groups`, //желательно вынести url в отдельную переменную "base_url", обычно я помещаю ее в store
				mode: 'cors',
				auth: {
					username: 'user',
					password: 'password',
				}
			};

			axios(config)
				.then((response) => {
					let groups = response.data
					for (let group of groups) {
						group.items = []
					}
					this.groups = groups
					this.get_a_list_of_items()
				})
				.catch(function (error) {
					console.log(error);
				})
		},
		get_a_list_of_items(group_id = false) {
			var config = {
				method: 'get',
				url: `http://62.217.182.170/items`,
				mode: 'cors',
				auth: {
					username: 'user',
					password: 'password',
				}
			};

			if (group_id) {
				config.url = `http://62.217.182.170/groups/${group_id}/items`
			}

			axios(config)
				.then((response) => {
					let items = response.data
					this.distribution_of_items_by_groups(items)
					this.generate_data_for_the_chart()
				})
				.catch(function (error) {
					console.log(error);
				})
		},

		distribution_of_items_by_groups(items) {
			items.filter((item) => {
				for (let group of this.groups) {
					if (item.id_group == group.id) {
						group.items.push(item)
					}
				}
			})
		},

		open_popup(title, description) {
			this.popup.title = title
			this.popup.description = description
			this.popup.visible = true

			console.log(title)
			console.log(description)
			
		},

		close_popup() {
			this.popup.visible = false
			this.popup.description = ''
		},
		generate_data_for_the_chart() {
			let labels = [];
			let items_count = []
			for (let group of this.groups) {
				labels.push(group.name)
				items_count.push(group.items.length)
			}

			this.chart_data.labels = labels
			this.chart_data.datasets[0].data = items_count
		}
	}

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.wrapper {
	width: 100%;
	height: 100vh;
	margin: 0;
	perspective: 900;
	overflow-y: scroll;
	background-color: #f6483b;
	font-family: "Titillium Web", sans-serif;
	color: rgba(48, 69, 92, 0.8);
}

.accordion-menu {
	display: inline-block;
	position: relative;
	left: 50%;
	margin: 150px 0;
	transform: translate(-50%, 0);
	min-width: 300px;
	max-width: 500px;
	padding: 10px 20px 20px;
	border-radius: 5px;
}

h1 {
	width: 100%;
	text-align: center;
	color: rgba(0, 0, 0, 0.71);
}

h2 {
	font-size: 18px;
	line-height: 34px;
	font-weight: 500;
	letter-spacing: 1px;
	display: block;
	margin: 0;
	cursor: pointer;
	color: #6c6c6a;
}


ul {
	list-style: none;
	perspective: 900;
	padding: 0 20px 10px;
	margin: 0;
	background-color: #fff;
	border-radius: 5px;
	box-shadow: 0 2px 5px 0 rgba(0, 0, 0, 0.2),
		0 2px 2px 0 rgba(255, 255, 255, 0.19);
}

ul li {
	position: relative;
	padding: 0;
	margin: 0;
	padding-bottom: 4px;
	padding-top: 18px;
	border-top: 1px dotted #dce7eb;
	cursor: pointer;
}

ul li:nth-child(1) {
	border: none;
	margin-bottom: 20px
}

ul li:nth-of-type(1) {
	animation-delay: 0.5s;
}

ul li:nth-of-type(2) {
	animation-delay: 0.75s;
}

ul li:nth-of-type(3) {
	animation-delay: 1.0s;
}

ul li:last-of-type {
	padding-bottom: 15px;
}


.diagram {
	position: relative;
	background-color: white;
	margin: 0 auto;
}

.diagram-container {
	width: 100%;
	margin-bottom: 30px;
}
</style>






