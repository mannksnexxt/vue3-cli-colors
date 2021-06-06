<template>
	<div class="container">
		<div class="pickers">
			<PickerList
				v-for="list in lists"
				:list="list"
				:key="list.id"
			/>
		</div>
								
		<div class="views">
			
			<ViewList
				v-for="list in lists"
				:list="list"
				:key="list.id" />
			
		</div>
	</div>
	
</template>



<script>
import PickerList from '@/components/picker/PickerList';
import ViewList from '@/components/view/ViewList';


let appLists =  [
	{
		id: 0,
		items: [
			{
				color: '#f1c40f',
				quantity: 12,
				selected: false
			},
			{
				color: '#2ecc71',
				quantity: 8,
				selected: false
			},
			{
				color: '#3498db',
				quantity: 32,
				selected: false
			},
			{
				color: '#9b59b6',
				quantity: 1,
				selected: false
			}
		]
	},
	{
		id: 1,
		items: [
			{
				color: '#f1c40f',
				quantity: 12,
				selected: false
			},
			{
				color: '#2ecc71',
				quantity: 8,
				selected: false
			},
			{
				color: '#3498db',
				quantity: 32,
				selected: false
			},
			{
				color: '#9b59b6',
				quantity: 0,
				selected: false
			}
		]
	},
	{
		id: 2,
		items: [
			{
				color: '#e74c3c',
				quantity: 40,
				selected: false
			},
			{
				color: '#e67e22',
				quantity: 7,
				selected: false
			},
			{
				color: '#bdc3c7',
				quantity: 12,
				selected: false
			},
			{
				color: '#34495e',
				quantity: 0,
				selected: false
			}
		]
	},
	{
		id: 3,
		items: [
			{
				color: '#3498db',
				quantity: 1,
				selected: false
			},
			{
				color: '#1abc9c',
				quantity: 8,
				selected: false
			},
			{
				color: '#fd79a8',
				quantity: 60,
				selected: false
			},
			{
				color: '#6c5ce7',
				quantity: 24,
				selected: false
			}
		]
	},
];


export default {
	name: 'App',
	data() {
		return {
			lists: appLists
		}
	},
	components: {
		PickerList,
		ViewList
	}
}

</script>



<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300&display=swap');

* {
	box-sizing: border-box;
	padding: 0;
	margin: 0;
	font-family: 'Montserrat', sans-serif;
}
button, label {
	cursor: pointer;
	transition: .1s;
}
li {
	list-style-type: none;
}

.container {
	width: 100%;
	min-height: 100vh;
	padding: 32px 64px;
	display: grid;
	gap: 100px;
	grid-template-columns: 1fr 1fr;
}
.pickers, .views {
	display: flex;
	flex-direction: column;
	gap: 20px;
	padding: 30px;
	box-shadow: 1px 3px 12px -2px rgba(34, 60, 80, 0.18);
}
[v-cloak] {
    display: none;
}


//animations
.slide-enter-active, .slide-leave-active {
	transition: .2s;
  }
.slide-enter-from, .slide-leave-to {
	opacity: 0;
	transform: translateX(-100px);
}

.flip-enter-active, .flip-leave-active {
	transition: .3s;
  }
.flip-enter-from, .flip-leave-to {
	opacity: 0;
	transform: rotateX(90deg);
}
</style>
