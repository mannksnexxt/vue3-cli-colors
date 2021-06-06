<template>
	<div class="picker">
		<header class="picker__header">
			<label class="picker__switcher">
				<input type="checkbox" v-model="isOpen">
				<i v-if="isOpen" class="fas fa-chevron-right"></i>
				<i v-else class="fas fa-chevron-down"></i>
			</label>
			
			<PickerListCheckbox
				@checkbox-change="changeAllItems"
				:index="list.id"
				:class="{ 'picker__checkbox--half-full': isHalfFull }"
				:checked="isFull"
			/>
		</header>
		
		<transition name="slide">
			<PickerListItems
				v-show="isOpen"
				:items="list.items"
			/>
		</transition>
	</div>
</template>




<script>
import PickerListCheckbox from '@/components/picker/PickerListCheckbox';
import PickerListItems from '@/components/picker/PickerListItems';


export default {
	props: {
		list: {
			type: Object,
			required: true
		}
	},
	data() {
		return {
			isOpen: false,
			isFiltered: true
		}
	},
	components: {
		PickerListCheckbox,
		PickerListItems
	},
	methods: {
		changeAllItems() {
			const checkedItems = this.list.items.filter(item => item.selected === true);
			if (!checkedItems.length || this.isHalfFull) {
				this.list.items.forEach(item => item.selected = true);
				return;
			}
			this.list.items.forEach(item => item.selected = false);
			
		}
	},
	computed: {
		isHalfFull() {
			if (this.checkedItemsLength && this.list.items.length !== this.checkedItemsLength) {
				return true;
			}
			return false;
		},
		isFull() {
			return this.checkedItemsLength === this.list.items.length;
		},
		checkedItemsLength() {
			return this.list.items.filter(item => item.selected === true).length;
		}
	}
}
</script>





<style lang="scss">
$switcherColor: #57606f;

.picker {
	display: flex;
	flex-direction: column;
	gap: 20px;
	
	&__header {
		display: flex;
		align-items: center;
		gap: 20px;
	}
	&__items {
		padding-inline-start: 80px;
		display: flex;
		flex-direction: column;
		gap: 12px;
	}
	&__item {
		display: flex;
		align-items: center;
		justify-content: space-between;
	}
	&__options {
		display: flex;
		align-items: center;
		gap: 12px;
	}
	&__input {
		height: 27px;
		border: none;
		&-number {
			max-width: 50px;
			text-align: right;
			font-size: 16px;
		}
		&-color {
			cursor: pointer;
			width: 25px;
			padding: 0;
			background: transparent;
			-webkit-appearance: none;
			&::-webkit-color-swatch-wrapper {
				padding: 0;
			}
			&::-webkit-color-swatch {
				padding: 0;
			}
		}
	}
}
.picker__switcher {
	color: $switcherColor;
	height: 25px;
	width: 25px;
	display: flex;
	justify-content: center;
	align-items: center;
	input {
		display: none;
	}
	i {
		font-size: 18px;
	}
	&:hover {
		opacity: .5;
	}
}
</style>