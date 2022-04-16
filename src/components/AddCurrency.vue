<template>
	<form @submit.prevent="onSubmit">
		<select name="LeaveType" @change="onChange" v-model="selectedValue">
			<option v-for="currency of currenciesList" v-bind:value="currency.Cur_Abbreviation">{{currency.Cur_Abbreviation}}</option>
		</select>
		<button type="submit">Add Currency</button>
	</form>
</template>

<script>
	export default {
		props: ["currenciesList"],

		data() {
			selectedValue: ""
		},

		methods: {
			onChange(event) {
				event.target.value;
			},

			onSubmit() {
				 if (this.selectedValue) {
					 currenciesList.map(({Cur_ID, Cur_OfficialRate}) => {
						 const newCurrency = {
							Cur_ID, 
						 	Cur_Abbreviation: this.selectedValue,
							Cur_OfficialRate
					 }
					 })
					 
					 this.$emit("add-currency", newCurrency)
				 }
			}			
		}
	}
			
		
	
</script>