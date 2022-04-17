<template>
	<li>
		<div class="flex">
			<span class="currency-name"><strong>{{currency.Cur_Abbreviation}}</strong></span>
			<span class="second-currency-name">{{currency.Cur_Name}}</span>
			<span class="sum">{{currency.Cur_OfficialRate}}</span>
		</div>
		<div>
			<a-button type="danger" ghost @click="$emit('remove-currency', currency.Cur_ID)">Удалить</a-button>
		</div>	
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

<style scoped>
	li {
		max-width: 550px;
		margin: 0 auto;
		font-size: 20px;
		padding: 1rem;
		border-bottom: 1px solid rgba(0, 0, 0, 0.3);
		background: rgb(197, 222, 236);
	}

	.flex {
		display: flex;
		justify-content: space-between;
		margin-bottom: 1rem;
		flex-wrap: wrap;
	}

	.currency-name {
		margin-right: 1rem;
	}

	.second-currency-name {
		margin-right: 1rem;
		justify-content: flex-start;
		color: rgb(3, 80, 73);
	}

	.sum {
		color: rgb(44, 52, 167);
	}

	@media screen and (max-width: 424.75px) {
		.flex {
			flex-direction: column;
		
		}

		.currency-name {
			margin-right: 0;
		}

		.second-currency-name {
			margin-right: 0;
		}
	}
</style>

