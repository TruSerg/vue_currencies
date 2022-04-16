<template>
 <div>
	 <h1>Currencies</h1>
	 <!-- <AddCurrency
	 	@add-currency="addCurrency" 
	 	v-bind:currenciesList="currenciesList"
	 /> -->

	 <form @submit.prevent="onSubmit">
		<select name="LeaveType" @change="onChange" v-model="selectedValue">
			<option v-for="currency of currenciesList" v-bind:value="currency.Cur_Abbreviation">{{currency.Cur_Abbreviation}}</option>
		</select>
		<button type="submit">Add Currency</button>
	</form>

	 <CurrenciesList 
	 	v-bind:newCurrenciesList="newCurrenciesList"
		@remove-currency="removeCurrency"
	 />
	  <!-- <div class="baseCurrensies">
		 <div v-for="currency of newCurrenciesList" >
		 	<h4>1 {{currency.Cur_Abbreviation}} - {{currency.Cur_OfficialRate}} BLR</h4>
		 </div>
	 </div> 
			  <div v-for="currency of currenciesList">
		 
		 <h4>1 {{currency.Cur_Abbreviation}} - {{currency.Cur_OfficialRate}} BLR</h4></div> -->
		
 </div>
 
</template>

<script>
import CurrenciesList from "@/components/CurrenciesList";
// import AddCurrency from "@/components/AddCurrency";

export default {
	name: "App",

	data() {
		return {
			currenciesList: [],
			newCurrenciesList: [],
			selectedValue: ""
		}
	},

	methods: {
		getCurrencies() {
			fetch("https://www.nbrb.by/api/exrates/rates?periodicity=0")
			.then(response => response.json())
			.then(json =>  {
				this.currenciesList = json

				this.currenciesList.filter(currency => {
					if (currency.Cur_Abbreviation === "USD" || currency.Cur_Abbreviation === "RUB" || currency.Cur_Abbreviation === "EUR") {
						return this.newCurrenciesList.push(currency)
					}
				})
			})
		},
		
		removeCurrency(Cur_ID) {
			this.newCurrenciesList = this.newCurrenciesList.filter(currency => currency.Cur_ID !== Cur_ID)
		},

		onChange(event) {
				event.target.value;
			},

		onSubmit() {
				
			

		},

		// addCurrency(newCurrency) {
		// 	this.newCurrenciesList.push(newCurrency)
		// },
	},

	mounted() {
		this.getCurrencies();
	},

	components: {
		CurrenciesList,
		// AddCurrency
  },

	
}
</script>

<style>
.baseCurrensies {
	margin-bottom: 50px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
