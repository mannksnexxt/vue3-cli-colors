<template>
	<li class="picker__item">
		<PickerListCheckbox
			@checkbox-change="item.selected = !item.selected"
			:index="index"
			:checked="item.selected"
		/>

		<div class="picker__options">
			<input
				v-model.number.lazy="item.quantity"
				@change="validateNumber"
				class="picker__input picker__input-number"
				type="number"
				min="0">
			<input 
				v-model="item.color"
				type="color"
				class="picker__input picker__input-color">
		</div>
	</li>
</template>


<script>
import PickerListCheckbox from '@/components/picker/PickerListCheckbox';

export default {
	props: {
		item: {
			type: Object,
			required: true
		},
		index: {
			type: Number,
			required: true
		}
	},
	components: {
		PickerListCheckbox
	},
	methods: {
		validateNumber() {
			if (!this.item.quantity || this.item.quantity < 0) {
				this.item.quantity = 0;
			}
		},
	}
}
</script>