<template>    
    <form @submit.prevent="handleSubmit">
        <label>Email:</label>
        <input v-model="email" type="email" required>

        <label>password:</label>
        <input v-model="password" type="password" required> 
        <input v-model="showPass" type="checkbox" style="margin-top: 10px;"> <span style="font-size: 11px;">Show password</span>
        <p v-if="showPass" style="border-bottom: 1px solid #ddd;">{{password}}</p>   
        <p v-if="passwordError" class="error">{{passwordError}}</p>       
        <br>
        <label>Role</label>    
        <select v-model="rol">
            <option value="developer">Web Developer</option>
            <option value="Designer">Web Designer</option>
        </select>

        <label>Skills (press spacebar or enter to add a skill)</label>
        <input v-model="tempSkill" @keypress="addSkill" type="text">

        <div class="terms">
            <input v-model="terms" type="checkbox" required>
            <label>Accept terms and conditions</label>
        </div>

        <div v-for="skill in skills" :key="skill" class="pill">
            <span @click="deleteSkill(skill)">{{skill}} <i class="bi bi-x"></i></span>
        </div>

     <div class="submit">
        <button>Create an account</button>
     </div>

    </form> 
<!--
        <div>
            <input v-model="names" value="Guille" type="checkbox">
            <label>Guille</label>
        </div>
        <div>
            <input v-model="names" value="July" type="checkbox">
            <label>July</label>
        </div>
        <div>
            <input v-model="names" value="Bella" type="checkbox">
            <label>Bella</label>
        </div>
     
--> 

    <p>Email: {{email}}</p> 
    
    <p>rol: {{rol}}</p>
    <p>Terms accepted: {{terms}}</p>
  
 <!-- <p>Name array: {{names}}</p>-->   
</template>

<script>
    export default {
        data(){
            return{
                email: '',
                password: '',
                rol: 'Designer',
                terms: false,
                tempSkill: '',
                skills: [],
                passwordError: '',
                showPass: false
               
            }
        },
        methods:{
            addSkill(e){
                if(e.key === ' ' || e.key === 'Enter' && this.tempSkill){                    
                    if(!this.skills.includes(this.tempSkill)){                                                 
                        this.skills.push(this.tempSkill)               
                    }    
                         
                    this.tempSkill = ''
                }
            },
            deleteSkill(skill){
                this.skills = this.skills.filter((item) => {
                    return skill !== item
                })
            },
            handleSubmit(){
                //validate password
                this.passwordError = this.passwordError > 5 ? 
                    '' : 'Password must be at least 6 char long'
            }
        }
    }
</script>

<style scoped>

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
    margin-top: 10px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
  }
  input, select {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
  }
  input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
  }
  .pill {
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
  button {
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
    cursor: pointer;
  }
  .submit {
    text-align: center;
  }
  .error {
    color: #ff0062;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
  }
  p{
    margin: 0;
  }

</style>