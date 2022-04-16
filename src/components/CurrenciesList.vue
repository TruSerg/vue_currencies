<template>
	<div>
		<ul>
			<CurrencyItem
				v-for="currency of newCurrenciesList"
				v-bind:currency="currency"
				v-on:remove-currency="removeCurrency"
			/>
		</ul>
	</div>
</template>

<script>
import CurrencyItem from "@/components/CurrencyItem"

	export default {
		props: ["newCurrenciesList"],

		methods: {
			removeCurrency(Cur_ID) {
				this.$emit("remove-currency", Cur_ID)
			}
		},

		components: {
			CurrencyItem
		}

	}
</script>
	

