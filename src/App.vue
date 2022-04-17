<template>
 <div>
	  <Header />
	  <div class="main-wrapper">
		 <h1 class="title">Валюты</h1>
	  <CurrenciesList 
	 	:baseCurrenciesList="baseCurrenciesList"
	  />

	  <AdditionalCarrensciesList 
	 	:class="{ show: isShow }"
	 	:additionalCurrenciesList="additionalCurrenciesList"
		@remove-currency="removeCurrency"
	  />
	  <div class="buttons">
		   <a-button type="primary" ghost @click="isShow=!isShow" class="btn">{{ btnText }}</a-button>
	  		<!-- <a-button type="primary" ghost @click="clearedLocalStorage">Показать все</a-button> -->
	  </div>
	</div>
	 	
 </div>
 
</template>

<script>
import CurrenciesList from "@/components/CurrenciesList";
import AdditionalCarrensciesList from "@/components/AdditionalCarrensciesList"
import Header from "@/components/Header"

export default {
	name: "App",

	data() {
		return {
			currenciesList: [],
			baseCurrenciesList: [],
			additionalCurrenciesList: [],
			isShow: true
		}
	},

	methods: {
		getCurrencies() {
			fetch("https://www.nbrb.by/api/exrates/rates?periodicity=0")
			.then(response => response.json())
			.then(json =>  {
				this.currenciesList = json

				this.currenciesList.filter(currency => {
					if (currency.Cur_Abbreviation === "USD" || currency.Cur_Abbreviation === "RUB" || currency.Cur_Abbreviation === "EUR" || currency.Cur_Abbreviation === "GBP") {
						return this.baseCurrenciesList.push(currency)
					}

					if (!(currency.Cur_Abbreviation === "USD" || currency.Cur_Abbreviation === "RUB" || currency.Cur_Abbreviation === "EUR" || currency.Cur_Abbreviation === "GBP")) {
						return this.additionalCurrenciesList.push(currency)
					}
				})
			})
		},

		removeCurrency(Cur_ID) {
			this.additionalCurrenciesList = this.additionalCurrenciesList.filter(currency => currency.Cur_ID !== Cur_ID)
			
			localStorage.setItem("additionalCurrenciesList", JSON.stringify(this.additionalCurrenciesList))
		},

		clearedLocalStorage() {
			
		}
	},


	 	computed: {
			btnText() {
				if(this.isShow) {
					return 'Показать больше'
				}
					return 'Скрыть'
		}
  },

	  	async mounted() {
			const data = await localStorage.getItem("additionalCurrenciesList")

			data ? this.additionalCurrenciesList = JSON.parse(data) : null
	},

	  mounted() {
			 this.getCurrencies();
		},

		components: {
			CurrenciesList,
			AdditionalCarrensciesList,
			Header
  	},	
}
</script>

<style scoped>
.show {
	display: none;
}

.title {
	text-align: center;
	margin-bottom: 1rem;
	color: rgb(0, 41, 128);
}

.buttons {
	text-align: center;
}

.main-wrapper {
	padding: 20px 15px;
	min-height: 100vh;
	background-color: #FFDEAD;
}

.btn {
	min-width: 150px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale; 
}
</style>
