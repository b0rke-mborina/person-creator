<template>
	<div class="home">
		<h1 class="mainTitle center">Get information about a person with a specific name</h1>
		<h3 class="subtitle center">Write a name:</h3>
		<div class="inputGroup">
			<v-text-field type="text" v-model="nameOfPerson"></v-text-field>
			<v-btn @click="fetchData(nameOfPerson)">Search</v-btn>
		</div>
		<v-data-table :headers="headers" :items="results" :hide-default-footer="true" class="resultsTable">
			
		</v-data-table>
	</div>
</template>

<script>
	const axios = require('axios')

	export default {
		name: 'Home',
		data() {
			return {
				nameOfPerson: null,
				results: [],
				headers: [
					{ text: "Name", value: "name", width: "15%", align: "center" },
					{ text: "Countries and probabilities", value: "countriesAndProbabilities", width: "30%", align: "center" },
					{ text: "Age", value: "age", width: "15%", align: "center" },
					{ text: "Gender", value: "gender", width: "15%", align: "center" },
					{ text: "Gender probability", value: "genderProbability", width: "15%", align: "center" }
				]
			}
		},
		methods: {
			async fetchData() {
				console.log(this.nameOfPerson);
				if (!this.nameOfPerson || this.nameOfPerson == "") {
					return alert("Field cannot be empty");
				}

				let nationalitiesAndProbabilities=[];
				let ageOfPerson=null;
				let genderAndProbability=null;


				const nationalities = await axios.get(
					"https://api.nationalize.io?name=" + this.nameOfPerson
				);
				console.log(nationalities.data);
				for (let country of nationalities.data.country) {
					console.log(country);
					let countryAndProbability=country.country_id + " - " + (country.probability*100).toFixed(2) + "%"
					nationalitiesAndProbabilities.push(countryAndProbability);
				}
				nationalitiesAndProbabilities=nationalitiesAndProbabilities.join("; \r\n")

				const age = await axios.get(
					"https://api.agify.io?name=" + this.nameOfPerson
				);
				console.log(age.data);
				ageOfPerson = age.data.age;
				console.log(ageOfPerson);


				const gender = await axios.get(
					"https://api.genderize.io?name=" + this.nameOfPerson
				);
				console.log(gender.data);
				genderAndProbability = {
					gender: gender.data.gender,
					probability: (gender.data.probability*100).toFixed(2) + "%",
				}
				console.log(genderAndProbability);

				// this.results=[];
				let finalResults = {
					name: this.nameOfPerson,
					countriesAndProbabilities: nationalitiesAndProbabilities || "not found",
					age: ageOfPerson || "not found",
					gender: genderAndProbability.gender || "not found",
					genderProbability: genderAndProbability.probability || "not found",
				}
				this.results.push(finalResults);
			}
		}
	}
</script>

<style scoped>
	.mainTitle {
		margin-top: 50px;
	}
	.subtitle {
		margin-top: 50px;
		margin-bottom: 10px;
	}
	.inputGroup {
		width: 30%;
		display: block;
		margin-left: auto;
		margin-right: auto;
		text-align: center;
	}
	.resultsTable {
		width: 75%;
		margin-left: auto;
		margin-right: auto;
		margin-top: 50px;
		text-align: center;
	}
	.resultsTable th {
		white-space: nowrap;
		white-space: pre;
	}
	.center {
		text-align: center;
	}
</style>