<template>
    <section class="container">
        <header>Register Form</header>
        <form action="#" class="form login" v-on:submit.prevent="validate" novalidate="true" autocomplete="off"
            id="Form">

            <div class="input-box">
                <label for="login__username">Full Name</label>
                <input type="text" name="username" placeholder="Username" id="username" class="form-control"
                    autocomplete="false" v-bind:class="{
                        'is-valid': validation.valid.username,
                        'is-invalid': validation.invalid.username
                    }" v-on:focus="clearValidation('username')" v-model="username" required />
            </div>
            <span class="valid-feedback" v-if="validation.valid.username">
                {{ validation.valid.username }}
            </span>

            <span class="invalid-feedback" v-if="validation.invalid.username">
                {{ validation.invalid.username }}
            </span>

            <div class="input-box">
                <label for="login__email">Email</label>
                <input type="text" name="email" placeholder="Email" id="email" class="form-control" autocomplete="false"
                    v-bind:class="{
                        'is-valid': validation.valid.email,
                        'is-invalid': validation.invalid.email
                    }" v-on:focus="clearValidation(email)" v-model="email" required />
            </div>
            <span class="valid-feedback" v-if="validation.valid.email">
                {{ validation.valid.email }}
            </span>

            <span class="invalid-feedback" v-if="validation.invalid.email">
                {{ validation.invalid.email }}
            </span>
            
            <div class="input-box">
                <label for="login__password">Password</label>
                <input type="password" name="password" placeholder="Password" id="password" class="form-control"
                    autocomplete="false" v-bind:class="{
                        'is-valid': validation.valid.password,
                        'is-invalid': validation.invalid.password
                    }" v-on:focus="clearValidation('password')" v-model="password" required />
            </div>
            <span class="valid-feedback" v-if="validation.valid.password">
                {{ validation.valid.password }}
            </span>

            <span class="invalid-feedback" v-if="validation.invalid.password">
                {{ validation.invalid.password }}
            </span>

            <div class="input-box">
                <label for="">Confirm Password</label>
                <input type="password" name="confirmPassword" placeholder="Confirm Password" id="confirmPassword"
                    class="form-control" autocomplete="false" v-bind:class="{
                        'is-valid': validation.valid.confirmPassword,
                        'is-invalid': validation.invalid.confirmPassword
                    }" v-on:focus="clearValidation('confirmPassword')" v-model="confirmPassword" required />
            </div>
            <span class="valid-feedback" v-if="validation.valid.confirmPassword">
                {{ validation.valid.confirmPassword }}
            </span>

            <span class="invalid-feedback" v-if="validation.invalid.confirmPassword">
                {{ validation.invalid.confirmPassword }}
            </span>

            <button>Submit</button>
        </form>
    </section>
</template>

<script>
export default {
    data() {
        return {
            username: '',
            email: '',
            password: '',
            confirmPassword: '',
            validation: {
                valid: {
                    username: '',
                    email: '',
                    password: '',
                    confirmPassword: ''
                },
                invalid: {
                    username: '',
                    email: '',
                    password: '',
                    confirmPassword: ''
                }
            }
        }
    },
    methods: {
        validate: function () {
            if (!this.username) {
                this.validation.valid.username = ''
                this.validation.invalid.username = 'Please enter your username.'
            } else if (this.username.length < 2) {
                this.validation.valid.username = ''
                this.validation.invalid.username = 'username should have min. 2 characters.'
            } else if (this.username.match(/[^a-z]/i)) {
                this.validation.valid.username = ''
                this.validation.invalid.username = 'username should contains only latin letters (a-z).'
            } else {
                this.validation.invalid.username = ''
                this.validation.valid.username = 'username is ready.'
            }

            if (!this.email) {
                 this.validation.valid.email = ''
                this.validation.invalid.email = 'Please enter your email.'
            }
             else if (this.email.match( /[^[^\s@]+@[^\s@]+\.[^\s@]+$]/i)) {
                 this.validation.valid.email = ''
                this.validation.invalid.email = 'Email should correct format.'
            } else {
                 this.validation.invalid.email = ''
                this.validation.valid.email = 'Email is ready.'
            }
            
            if (!this.password) {
                 this.validation.valid.password = ''
                this.validation.invalid.password = 'Please enter password.'
            } else if (this.password.length < 8) {
                this.validation.valid.password = ''
                this.validation.invalid.password = 'Password should have min. 8 characters.'
            } else if (this.password.match(/[^a-z]/i)) {
                this.validation.invalid.password = 'Password should contains only latin letters (a-z).'
            } else {
                this.validation.valid.password = 'Password is strong.'
                 this.validation.invalid.password = ''
            }

            
            if (!this.confirmPassword) {
                this.validation.valid.confirmPassword = ''
                this.validation.invalid.confirmPassword = 'Please enter confirm Password.'
            } else if (this.confirmPassword !== password.value) {
                this.validation.valid.confirmPassword = ''
                this.validation.invalid.confirmPassword = 'Confirm Password not match'
            }  else {
                this.validation.invalid.confirmPassword = ''
                this.validation.valid.confirmPassword = 'Confirm Password is correct.'
            }

            this.$forceUpdate()
        }
    },

    clearValidation(field) {
        this.validation.valid[field] = ''
        this.validation.invalid[field] = ''
        console.log('Valid:', this.validation.valid)
        console.log('Invalid:', this.validation.invalid)
    }
}
</script>

<style>
/* Import Google font - Poppins */
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@200;300;400;500;600;700&display=swap');

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Poppins', sans-serif;
    overflow: hidden;
}

body {
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 20px;
    margin-left: 340px;
    background: rgb(130, 106, 251);
}

.container {
    position: relative;
    max-width: 700px;
    width: 100%;
    background: #fff;
    padding: 35px;

    border-radius: 8px;
    box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
}

.container header {
    font-size: 1.5rem;
    color: #333;
    font-weight: 500;
    text-align: center;
}

.container .form {
    margin-top: 30px;
}

.form .input-box {
    width: 100%;
    margin-top: 20px;
}

.input-box label {
    color: #333;
}

.form :where(.input-box input, .select-box) {
    position: relative;
    height: 50px;
    width: 100%;
    outline: none;
    font-size: 1rem;
    color: #707070;
    margin-top: 8px;
    border: 1px solid #ddd;
    border-radius: 6px;
    padding: 0 15px;
}

.input-box input:focus {
    box-shadow: 0 1px 0 rgba(0, 0, 0, 0.1);
}

.form .column {
    display: flex;
    column-gap: 15px;
}

.form .gender-box {
    margin-top: 20px;
}

.gender-box h3 {
    color: #333;
    font-size: 1rem;
    font-weight: 400;
    margin-bottom: 8px;
}

.form :where(.gender-option, .gender) {
    display: flex;
    align-items: center;
    column-gap: 50px;
    flex-wrap: wrap;
}

.form .gender {
    column-gap: 5px;
}

.gender input {
    accent-color: rgb(130, 106, 251);
}

.form :where(.gender input, .gender label) {
    cursor: pointer;
}

.gender label {
    color: #707070;
}

.address :where(input, .select-box) {
    margin-top: 15px;
}

.select-box select {
    height: 100%;
    width: 100%;
    outline: none;
    border: none;
    color: #707070;
    font-size: 1rem;
}

.form button {
    height: 55px;
    width: 100%;
    color: #fff;
    font-size: 1rem;
    font-weight: 400;
    margin-top: 30px;
    border: none;
    cursor: pointer;
    transition: all 0.2s ease;
    background: rgb(130, 106, 251);
}

.form button:hover {
    background: rgb(88, 56, 250);
}

/*Responsive*/
@media screen and (max-width: 500px) {
    .form .column {
        flex-wrap: wrap;
    }

    .form :where(.gender-option, .gender) {
        row-gap: 15px;
    }
}

.valid-feedback {
    color: rgb(0, 255, 0);
}

.invalid-feedback {
    color: red;
}
</style>
