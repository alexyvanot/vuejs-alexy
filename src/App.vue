<script>
export default {
	data: function () {
		return {
			date: null,
			montant: null,
			description: null,
			transactions: [],
			errorMsg: null,
		};
	},

	methods: {
		add: function () {
			if(!this.date || !this.amount || !this.description) {
				this.errorMsg = "You have to fill up infos";
				return alert(this.errorMsg);
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

		remove: function(idx) {
			this.transactions.splice(idx, 1);
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
			<tr v-for="(t, idx) in transactions" v-bind:key="t.id">
				<td>
					{{ formatDate(t.date) }}
				</td>
				<td>
					{{ t.montant }}
				</td>
				<td>
					{{ t.description }}
				</td>
				<button v-on:click="remove(idx)">Delete</button>
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
		<span v-if="errorMsg">Error: {{errorMsg}}</span>
	</header>
</template>

<style></style>
