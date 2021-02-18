<template>
	<form @submit.prevent="handleSubmit">
		<label>Email:</label>
		<input type="email" required v-model="email">

		<label>Password:</label>
		<input type="password" required v-model="password">
		<div v-if="passwordError" class="error">{{ passwordError }}</div>

		<label>Role:</label>
		<select v-model="role">
			<option value="developer">Web developer</option>
			<option value="designer">Web Designer</option>
		</select>

		<label>Skills</label>
		<input type="text" v-model="tempSkill" placeholder="separated by ," @keyup="addSkill">
		<div v-for="skill in skills" :key="skill" class="pill" @click="deleteSkill(skill)">{{ skill }}</div>

		<div class="terms">
			<input type="checkbox" v-model="terms" required>
			<label>Accept terms and conditions</label>
		</div>

		<div class="submit">
			<button>Create an account</button>
		</div>

	</form>

	<p>Email: {{ email }}</p>
	<p>Password: {{ password }}</p>
	<p>Role: {{ role }}</p>
	<p>Terms: {{ terms }}</p>
</template>

<script>
export default {
	data() {
		return {
			email: '',
			password: '',
			role: 'designer',
			passwordError: '',
			tempSkill: '',
			skills: [],
			terms: false,
		}
	},
	methods: {
		addSkill(e) {
			if (e.key === ',') {
				if (this.tempSkill.length != 1) {
					let skill = this.tempSkill.slice(0,-1)
					if (this.skills.indexOf(skill) == -1) {
						this.skills.push(skill);
					}
				}
				this.tempSkill = '';
			}
		},
		deleteSkill(skill) {
			this.skills = this.skills.filter(el => el != skill)
		},
		handleSubmit() {
			this.passwordError = this.password.length >= 8 ?
			'' : 'Password must contain at least 8 characters'
		}
	}
}
</script>

<style>
	form {
		max-width: 420px;
		margin: 30px auto;
		background: white;
		text-align: left;
		padding: 40px;
		border-radius: 10px;
	}

	label {
		color: #aaa;
		display: inline-block;
		margin: 25px 0 15px;
		font-size: 0.7em;
		text-transform: uppercase;
		letter-spacing: 1px;
		font-weight: bold;
	}

	input,select {
		display: block;
		padding: 10px 6px;
		width: 100%;
		box-sizing: border-box;
		border: none;
		border-bottom: 1px solid #ddd;
		color: #555;
	}
	input:focus,
	select:focus {
		outline: none;
		border-bottom: 2px solid #ccc;
	}

	input[type='checkbox'] {
		display: inline-block;
		width: 16px;
		margin: 0 10px 0 0;
		position: relative;
		top: 2px;		
	}

	.pill {
		display: inline-block;
		margin: 20px 10px 0 0;
		padding: 6px 15px;
		background: #eee;
		border-radius: 5px;
		font-size: 12px;
		letter-spacing: 1px;
		font-weight: bold;
		color: #777;
		cursor: pointer;
	}

	button {
		background: #0b6dff;
		border: 0;
		padding: 10px 20px;
		margin-top: 20px;
		color: white;
		border-radius: 20px;
		cursor: pointer;
	}

	button:focus {
		outline: none;
	}

	.submit {
		text-align: center;
	}

	.error {
		margin-top: 10px;
		color: #ff0062;
		font-size: .8em;
		font-weight: bold;
	}
</style>
