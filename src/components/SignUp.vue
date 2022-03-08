<template>
  <form @submit.prevent="submitForm">
		<label>Email: </label>
		<input type="email" required v-model="email" />
		<label>Password: </label>
		<input type="password" required v-model="password" />
		<div v-if="passwordError" class="error">{{passwordError}}</div>
		<label>Role: </label>
		<select v-model="role">
			<option value="Web Design">Web Design</option>
			<option value="Web Dev">Web Dev</option>
		</select>

		<label>Skills:</label>
		<input type="text" v-model="skillTemps" @keyup.alt="addSkill">
		<div v-for="skill in skills" :key="skill" class="pill" >
			<span @click="deleteSkill(skill)">{{skill}}</span>
		</div>

		<div class="terms">
			<input type="checkbox" v-model="terms" required>
			<label>Accept terms</label>
		</div>

		<!-- <div>
			<input type="checkbox" value="Shaun" v-model="names">
			<label>Shaun</label>
		</div>
		<div>
			<input type="checkbox" value="Yoshi" v-model="names">
			<label>Yoshi</label>
		</div>
		<div>
			<input type="checkbox" value="Mario" v-model="names">
			<label>Mario</label>
		</div> -->

		<div class="submit">
			<button>Create Account</button>
		</div>

	</form>
	<!-- <p>Email: {{ email }}</p>
	<p>Pass: {{ password }}</p>
	<p>Role: {{ role }}</p>
	<p>Terms: {{ terms }}</p>
	<p>Names: {{ names }}</p> -->
	
</template>

<script>
export default {
	data() {
		return {
			email: "",
			password: "",
			role:'',
			terms:false,
			names:[],
			skillTemps:'',
			skills:[],
			passwordError:''
		};
	},
	methods:{
		addSkill(e){
			if(e.key===',' && this.skillTemps){
				if(!this.skills.includes(this.skillTemps)){
					this.skills.push(this.skillTemps)
				}
				this.skillTemps=''
			}
		},
		deleteSkill(skill){
			this.skills = this.skills.filter((item)=>{
				return skill !== item
			})
		},
		submitForm(){
			//validate pass
			this.passwordError = this.password.length > 5 ? 
				'' : 'too short'

			if(!this.passwordError){
				console.log('email: ', this.email)
				console.log('password: ', this.password)
				console.log('role: ', this.role)
				console.log('skills: ', this.skills)
				console.log('terms: ', this.terms)
			}
		}
	}
};
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
	font-size: 0.6em;
	text-transform: uppercase;
	letter-spacing: 1px;
	font-weight: bold;
}
input {
	display: block;
	padding: 10px 6px;
	width: 100%;
	box-sizing: border-box;
	border: none;
	border-bottom: 1px solid #ddd;
	color: #555;
}
select{
	display: block;
	padding: 10px 6px;
	width: 100%;
	color: #555;
	border: 1px solid #ddd;
	outline: none;
}
input[type="checkbox"]{
	display: inline-block;
	width: 16px;
	margin: 0 10px 0 0;
	position: relative;
	top: 2px;
}
.pill{
	display: inline-block;
	margin: 20px 10px 0 0;
	padding: 6px 12px;
	background: #eee;
	border-radius: 20px;
	font-size: 12px;
	letter-spacing: 1px;
	font-weight: bold;
	color: #777;
	cursor: pointer;
}
button{
	background: rgb(49, 49, 221);
	border: 0;
	padding: 10px 20px;
	color: white;
	border-radius: 20px;
}
.submit{
	text-align: center;
}
.error{
	color: rgb(255, 0, 119);
	margin-top: 10px;
	font-size: 0.8em;
	font-weight: bold;
}
</style>
