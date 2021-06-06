<template>
	<ul class="picker__items">
		<PickerListItem
			v-for="(item, index) in items"
			:item="item"
			:index="index"
			:key="item"
		/>
	</ul>
</template>


<script>
import PickerListItem from '@/components/picker/PickerListItem';

export default {
	props: {
		items: {
			type: Array,
			required: true
		}
	},
	components: {
		PickerListItem
	}
}
</script>