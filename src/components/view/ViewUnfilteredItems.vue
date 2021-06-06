<template>
	<div v-show="selectedItems.length">
		<div class="view__colors-row" >
			<div
				class="view__color"
				v-for="item in selectedItems"
				:key="item.id"
				:style="{ background: item.color }"
				@click="reduceColor(item.color)"
				>
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
	data() {
		return {
			random: []
		}
	},
	methods: {
		getUniqueID() {
			return '_' + Math.random().toString(36).substr(2, 9);
		},
		reduceColor(color) {
			const reducedColor = this.list.items.find(item => item.color === color);
			reducedColor.quantity--;
		},
	},
	computed: {
		selectedItems() {
			const randomColorsArr = [];
			const selectedArr = this.list.items.filter( item => item.selected === true );

			selectedArr.forEach(item => {
				for (let i = 1; i <= item.quantity; i++) {
					randomColorsArr.push({
						id: this.getUniqueID(),
						color: item.color
					});
				}
			})
			return randomColorsArr;
		}
	}
}
</script>