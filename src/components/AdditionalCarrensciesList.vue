<template>
	<div>
		<ul>
			<AdditionalItem
				v-for="currency of additionalCurrenciesList"
				:currency="currency"
				@remove-currency="removeCurrency"
			/>
		</ul>
	</div>
</template>

<script>
import AdditionalItem from "@/components/AdditionalItem"

	export default {
		props: ["additionalCurrenciesList"],

		methods: {
			removeCurrency(Cur_ID) {
				this.$emit("remove-currency", Cur_ID)
			}	
		},

		components: {
			AdditionalItem
		}
	}	
</script>

<style scoped>
	ul {
		list-style: none;
		margin: 0;
		padding: 0;
		margin-bottom: 2rem;
	}
</style>