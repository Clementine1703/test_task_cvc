<template>
	<div class="popup-wrapper" v-if="popup.visible" @click="close_popup()">
        <div class="popup" @click.stop>
            <div class="popupContent" id="popupPopup">
                <button class="close" @click="close_popup()">✖</button>
                <p cla> <b>{{ popup.title }}</b> <br> {{ popup.description }}</p>
            </div>
        </div>
    </div>
</template>

<script>

export default {
	name: 'ModalWindow',
	props: ['popup'],
	components: {
	},
	methods:{
		close_popup(){
			this.$emit('closepopup')
		}
	}
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.popup-wrapper {
	width: 100%;
	height: 100vh;
	position: absolute;
	background-color: #000000aa;
	z-index: 999;
	left: 0;
	top: 0;
	display: flex;
	align-items: center;
	justify-content: center;
}
.popupContent {
	width: 320px;
	display: flex;
	flex-direction: column;
	align-items: center;
	background-color: #fff;
	color: #000;
	text-align: center;
	border-radius: 20px;
	padding: 30px 30px 70px;
}

.popup button.close {
	width: 60px;
	font-size: 40px;
	color: #c0c5cb;
	align-self: flex-end;
	background-color: transparent;
	border: none;
	margin-bottom: 10px;
	cursor: pointer;
}

.popup button.close:hover {
	color: rgba(255, 0, 0, 0.678);
}

.popup p {
	margin-bottom: 40px;
    margin-top: 20px;
	font-size: 18px;
    line-height: 40px;
}
</style>






