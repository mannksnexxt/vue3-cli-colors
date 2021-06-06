<template>
	<div class="view">
		<header class="view__header">
			<h3>List {{ list.id + 1 }}</h3>
			<button class="view__button" @click="changeDisplayMode">
				<i v-if="component === 'ViewFilteredItems'" class="fas fa-random"></i>
				<i v-else class="fas fa-sort-alpha-down"></i>
			</button>
		</header>
		

		<div class="view__items">

			<transition name="flip" mode="out-in">
				<component :is="component" :list="list" :key="list.id" />
			</transition>

		</div>
		
	</div>
</template>


<script>
import ViewFilteredItems from '@/components/view/ViewFilteredItems';
import ViewUnfilteredItems from '@/components/view/ViewUnfilteredItems';


export default {
	props: {
		list: {
			type: Object,
			required: true
		}
	},
	components: {
		ViewFilteredItems,
		ViewUnfilteredItems
	},
	data() {
		return {
			component: 'ViewFilteredItems'
		}
	},
	methods: {
		changeDisplayMode() {
			if (this.component === 'ViewFilteredItems') {
				this.component = 'ViewUnfilteredItems';
			} else {
				this.component = 'ViewFilteredItems';
			}
		}
	}
}
</script>



<style lang="scss">
$buttonColor: #dfe4ea;

.view {
	display: flex;
	flex-direction: column;
	gap: 20px;
	&__header {
		display: flex;
		align-items: center;
		justify-content: space-between;
	}
	&__button {
		transition: .2s;
		padding: 0;
		border: none;
		background: transparent;
		color: #7f8c8d;
		font-size: 20px;
		&:hover {
			opacity: .7;
		}
	}
	&__items > div {
		display: grid;
		gap: 20px;
	} 
	&__colors-row {
		display: flex;
		flex-wrap: wrap;
		gap: 6px;
	}
	&__color {
		cursor: pointer;
		transition: .2s;
		height: 20px;
		width: 20px;
		&:hover {
			transform: scale(.9);
		}
	}
}
</style>