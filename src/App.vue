<script>
export default {
	data: function () {
		return {
			date: null,
			montant: null,
			description: null,
			transactions: [],
		};
	},

	methods: {
		add: function () {
			if(!this.date || !this.amount || !this.description) {
				return this.errorMsg = "You have to fill up infos"
			}
			this.transactions
			.push({
				date: this.date,
				montant: this.amount,
				description: this.description,
			});

			// Reset for next instance
			["date", "amount", "description", "errorMsg"].forEach(
				(obj) => (this[obj] = null)
			);
		},

		formatDate: function(date) {
			return new Intl.DateTimeFormat('fr-FR').format(new Date(date));
		},
	},
};
</script>

<template>
	<table>
		<thead>
			<tr>
				<th>Date</th>
				<th>Montant</th>
				<th>Description</th>
			</tr>
		</thead>
		<tbody>
			<tr v-for="t in transactions">
				<td>
					{{ formatDate(t.date) }}
				</td>
				<td>
					{{ t.montant }}
				</td>
				<td>
					{{ t.description }}
				</td>
			</tr>
		</tbody>
	</table>
	<header>
		<div>
			Date: <input type="date" v-model="date" /> <br />
			Montant: <input type="number" v-model="amount" /> <br />
			Description: <input type="text" v-model="description" /> <br />
			<button v-on:click="add">Save</button>
		</div>
	</header>
</template>

<style></style>
