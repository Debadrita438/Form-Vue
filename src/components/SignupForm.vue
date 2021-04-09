<template>
    <form>
        <label>Email:</label>
        <input type="email" required v-model='email'>

        <label>Password:</label>
        <input type="password" required v-model='pass'>
        <div v-if='passwordError' class='pass'>{{ passwordError }}</div>

        <label>Role:</label>
        <select v-model='role'>
            <option value="developer">Web Developer</option>
            <option value="designer">Web Designer</option>
        </select>

        <label>Skills: (Press alt+',' to seperate skills)</label>
        <input type="text" v-model='tempSkill' @keyup.alt="addSkill" >
        <div v-for= 'skill in skills' :key= 'skill' class= 'pill'>
            <span @click='deleteSkill(skill)'>{{ skill }}</span>
        </div>

        <div class="terms">
            <input type="checkbox" v-model='terms' required>
            <label>Accept Terms and Conditions</label>
        </div>

        <button class="submit" @click.prevent='handleSubmit'>Create An Account</button>

    </form>

</template>

<script>
    export default {
        data() {
            return {
                email: '',
                pass: '',
                role: 'developer',
                terms: false,
                tempSkill: '',
                skills: [],
                passwordError: ''
            }
        },
        methods: {
            addSkill(event) {
                if(event.key === ',' && this.tempSkill) {
                    if(!this.skills.includes(this.tempSkill)) {
                        this.skills.push(this.tempSkill)
                    }
                    this.tempSkill = ''
                }
            },
            deleteSkill(skill) {
                this.skills = this.skills.filter((item) => { 
                    return item != skill
                })
            },
            handleSubmit() {
                // validate password
                this.passwordError = this.pass.length > 5 ? '' : 'Password must be at least 6 characters long'
                if(!this.passwordError) {
                    console.log("Email: ",this.email)
                    console.log("Password: ",this.pass)
                    console.log("Role: ",this.role)                    
                    console.log("Skills: ",this.skills)                    
                    console.log("Terms Accepted: ",this.terms)                    

                }
            }
        }
    }
</script>

<style>
    form {
        max-width: 420px;
        margin: 30px auto;
        background: #21252b;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
    }

    label {
        color: #c9d1d9;
        display: inline-block;
        margin: 25px 0 15px;
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
        border-radius: 4px;
        border-style: groove;
        border-width: 2px;
        border-color: #767676;
        color: #c9d1d9;
        background-color: #0d1117;
        box-shadow: none;
        outline: none;
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
        padding: 6px 12px;
        background: #767676;
        border-radius: 20px;
        font-size: 12px;
        letter-spacing: 1px;
        font-weight: bold;
        color: #c9d1d9;
        cursor: pointer;
    }

    .terms {
        padding-bottom: 40px;
    }

    button {
        display: block;
        background: #0d1117;
        border-radius: 2px;
        padding: 10px 20px;
        color: #c9d1d9;
        border-radius: 20px;
        margin: 0 auto;
        border-style: groove;
        border-color: #767676;
    }

    .submit {
        text-align: center;
        text-transform: uppercase;
        font-weight: bold;
        letter-spacing: 1px;
    }

    .pass {
        color: #c9d1d9;
        font-size: 0.6em;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
        padding-top: 10px;
    }
</style>