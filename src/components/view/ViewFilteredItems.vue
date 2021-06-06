<template>
	<div v-show="selectedItems.length">
		<div class="view__colors-row" v-for="item in selectedItems" :key="item.id">
			<div
				class="view__color"
				v-for="color in item.quantity"
				:key="color"
				:style="{ background: item.color }"
				@click="reduceColor(item.color)">
			</div>
		</div>		
	</div>
</template>

<script>

export default {
	props: {
		list: {
			type: Object,
			required: true
		},
	},
	methods: {
		getUniqueID() {
			return '_' + Math.random().toString(36).substr(2, 9);
		},
		reduceColor(color) {
			const reducedColor = this.list.items.find(item => item.color === color);
			reducedColor.quantity--;
		}
	},
	computed: {
		selectedItems() {
			const selectedArr = this.list.items.filter( item => item.selected === true );
			return selectedArr.map( item => {
				item.id = this.getUniqueID();
				return {
					id: this.getUniqueID(),
					...item
				}
			})
		}
	},
}
</script>