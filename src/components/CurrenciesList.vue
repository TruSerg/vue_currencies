<template>
	<div class="currencies-list">
		<ul>
			<CurrencyItem
				v-for="currency of baseCurrenciesList"
				:currency="currency"
			/>
		</ul>
	</div>
</template>

<script>
import CurrencyItem from "@/components/CurrencyItem"

	export default {
		props: {
			baseCurrenciesList: {
				type: Array,
				required: true
			},
		},

		components: {
			CurrencyItem
		}

	}
</script>

<style scoped>
  .currencies-list {
    width: 100%;
  }

	ul {
		list-style: none;
		margin: 0;
		padding: 0;
		margin-bottom: 2rem;
	}
</style>
	

