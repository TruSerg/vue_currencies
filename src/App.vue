<template>
 <div>
	  <Header />
	  <div class="main-wrapper">
		 <h1 class="title">Currencies</h1>
      <div class="currencies-wrapper">
        <Loader class="loader" v-if="isLoading" />
        <CurrenciesList
            v-else="baseCurrenciesList"
            :baseCurrenciesList="baseCurrenciesList"
        />
      </div>

	  <AdditionalCarrensciesList
        :class="{ show: isShow }"
        :additionalCurrenciesList="additionalCurrenciesList"
        @remove-currency="removeCurrency"
	  />
	  <div class="buttons">
		   <a-button type="primary" ghost @click="isShow=!isShow" class="btn">{{ btnText }}</a-button>
	  </div>
	</div>
	 	
 </div>
 
</template>

<script>
import CurrenciesList from "@/components/CurrenciesList";
import AdditionalCarrensciesList from "@/components/AdditionalCarrensciesList"
import Header from "@/components/Header"
import Loader from "@/components/Loader"

export default {
	name: "App",

		data() {
			return {
				currenciesList: [],
				baseCurrenciesList: [],
				additionalCurrenciesList: [],
				isShow: true,
        isLoading: true,
			}
		},

		methods: {
			async getCurrencies() { 
				try {
				await fetch("https://www.nbrb.by/api/exrates/rates?periodicity=0")
						.then(response => response.json())
						.then(json =>  {
                this.currenciesList = json

                this.isLoading = false

						this.currenciesList.filter(currency => {
							if (currency.Cur_Abbreviation === "USD" || currency.Cur_Abbreviation === "RUB" || currency.Cur_Abbreviation === "EUR" || currency.Cur_Abbreviation === "GBP") {
								return this.baseCurrenciesList.push(currency)
							}

							if (!(currency.Cur_Abbreviation === "USD" || currency.Cur_Abbreviation === "RUB" || currency.Cur_Abbreviation === "EUR" || currency.Cur_Abbreviation === "GBP")) {
								return this.additionalCurrenciesList.push(currency)
						}
					})
				})

				} catch (error) {

				}
				
			},

			removeCurrency(Cur_ID) {
			   this.additionalCurrenciesList = this.additionalCurrenciesList.filter(currency => currency.Cur_ID !== Cur_ID)
				
				localStorage.setItem("additionalCurrenciesList", JSON.stringify(this.additionalCurrenciesList))
			},
		},

		

		mounted() {
      this.getCurrencies();

			const data = localStorage.getItem("additionalCurrenciesList")

			data ? this.additionalCurrenciesList = JSON.parse(data) : null
		},

	 	computed: {
			btnText() {
				if(this.isShow) {
					return 'Показать больше'
				}
					return 'Скрыть'
			}
  		},

		components: {
			CurrenciesList,
			AdditionalCarrensciesList,
			Header,
      Loader,
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
    color: #2690fe;
	}

  .loader {
    margin: 0 auto;
  }

	.buttons {
		text-align: center;
	}

	.main-wrapper {
		position: relative;
		padding: 20px 15px;
		min-height: 100vh;
		background-color: #FFDEAD;
	}

  .currencies-wrapper {
    max-width: 600px;
    min-height: 40vh;
    margin: 0 auto;
    display: flex;
    align-items: center;
    justify-content: center;
  }

	.btn {
		min-width: 150px;
	}

	#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale; 
	}

  @media(max-width: 424px) {
    .currencies-wrapper {
      min-height: 60vh;
    }
  }
</style>
