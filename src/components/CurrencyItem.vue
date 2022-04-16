<template>
	<li>
		<span>1 {{currency.Cur_Abbreviation}}</span>
		<span>{{currency.Cur_OfficialRate}}</span>
		<button v-on:click="$emit('remove-currency', currency.Cur_ID)">&times;</button>
	</li>
</template>

<script>
	export default {
		props: {
			currency: {
				type: Object,
				required: true,
			}
		}
	}
</script>