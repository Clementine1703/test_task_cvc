<template>
	<input type="checkbox" checked>
	<i class="arrow"></i>
	<h2><i class="fas fa-code"></i>{{ group.name }}</h2>
	<p v-for="item in group.items" :key="item.id" @click="open_popup(item.name, item.description)">
		{{ item.name }}
	</p>
</template>

<script>

export default {
	name: 'GroupItem',
	props: ['group'],
	components: {
	},
	methods:{
		open_popup(title, description){
			this.$emit('openpopup', title, description)
		}
	}
}

</script>

<!-- Add "scoped" attribute tomit CSS to this component only -->
<style scoped>

p {
	color: rgba(48, 69, 92, 0.8);
	font-size: 15px;
	line-height: 40px;
	letter-spacing: 1px;
	position: relative;
	overflow: hidden;
	max-height: 800px;
	opacity: 1;
	transform: translate(0, 0);
	z-index: 2;
	padding: 0 10px;
	margin-top: 6px;
}


p:hover {
	background-color: #dce7eb9f;
}

 .arrow {
	position: absolute;
	transform: translate(-6px, 0);
	margin-top: 6px;
	right: 0;
}

 .fas {
	color: #f6483b;
	font-size: 15px;
	margin-right: 10px;
}

 .arrow:before,
 .arrow:after {
	content: "";
	position: absolute;
	background-color: #f6483b;
	width: 3px;
	height: 9px;
}

 .arrow:before {
	transform: translate(-2px, 0) rotate(45deg);
}

 .arrow:after {
	transform: translate(2px, 0) rotate(-45deg);
}

 input[type=checkbox] {
	position: absolute;
	cursor: pointer;
	width: 100%;
	height: 100%;
	z-index: 1;
	opacity: 0;
}

 input[type=checkbox]:checked~p {
	margin-top: 0;
	max-height: 0;
	opacity: 0;
	transform: translate(0, 50%);
}

 input[type=checkbox]:checked~.arrow:before {
	transform: translate(2px, 0) rotate(45deg);
}

 input[type=checkbox]:checked~.arrow:after {
	transform: translate(-2px, 0) rotate(-45deg);
}

.transition,
p,
 .arrow:before,
 .arrow:after {
	transition: all 0.25s ease-in-out;
}

.flipIn,
h1
 {
	animation: flipdown 0.3s ease both;
}

.no-select,
h2 {
	-webkit-tap-highlight-color: transparent;
	-webkit-touch-callout: none;
	user-select: none;
}

@keyframes flipdown {
	0% {
		opacity: 0;
		transform-origin: top center;
		transform: rotateX(-90deg);
	}

	5% {
		opacity: 1;
	}

	80% {
		transform: rotateX(8deg);
	}

	83% {
		transform: rotateX(6deg);
	}

	92% {
		transform: rotateX(-3deg);
	}

	100% {
		transform-origin: top center;
		transform: rotateX(0deg);
	}
}

</style>






