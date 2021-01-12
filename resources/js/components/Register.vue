<style >
span.w-full.text-red-500 {
    background-color: #dc3545!important;
    color: white;
    display: inline-flex;
}
span.w-full.text-green-500 {
    background-color: #28a745!important;
    color: white;
    padding: 20px;
}
.w-full .text-green-500{
    display:none;
}


</style>
<template>
      
      <div class="flex flex-wrap w-full justify-center items-center pt-56">
        <div class="flex flex-wrap max-w-xl">
            <span class="w-full text-green-500"> You have registered successfully. </span>
            <div class="p-2 text-2xl text-gray-800 font-semibold"><h1>Register an account</h1></div>
            <div class="p-2 w-full">
                <label class="w-full" for="name">Name</label>
                <span class="w-full text-red-500" v-if="errors.name">{{errors.name[0]}}</span>
                <input class="w-full bg-gray-100 rounded border border-gray-400 focus:outline-none focus:border-indigo-500 text-base px-4 py-2" placeholder="Name" type="text" v-model="form.name" >
            </div>
            <div class="p-2 w-full">
                <label for="email">Your e-mail</label>
                <span class="w-full text-red-500" v-if="errors.email">{{errors.email}}</span>
                <input class="w-full bg-gray-100 rounded border border-gray-400 focus:outline-none focus:border-indigo-500 text-base px-4 py-2" placeholder="Email" type="email" v-model="form.email">
            </div>
            <div class="p-2 w-full">
                <label for="password">Password</label>
                <span class="w-full text-red-500" v-if="errors.password">{{errors.password}}</span>
                <input class="w-full bg-gray-100 rounded border border-gray-400 focus:outline-none focus:border-indigo-500 text-base px-4 py-2" placeholder="Password" type="password" v-model="form.password" name="password">
            </div>
            <div class="p-2 w-full">
                <label for="confirm_password">Confirm Password</label>
                <span class="w-full text-red-500" v-if="errors.password_confirmation">{{errors.password_confirmation}}</span>
                <input class="w-full bg-gray-100 rounded border border-gray-400 focus:outline-none focus:border-indigo-500 text-base px-4 py-2" placeholder="Confirm Password" type="password" v-model="form.password_confirmation" name="password_confirmation">
            </div>
            <div class="p-2 w-full mt-4">
                <button @click.prevent="saveForm" type="submit" class="flex text-white bg-indigo-500 border-0 py-2 px-8 focus:outline-none hover:bg-indigo-600 rounded text-lg">Register</button>
            </div>
        </div> 
    </div>
</template>
<script>
import { required, email, minLength, sameAs } from "vuelidate/lib/validators";

export default {
    name: "app",
    data(){
        return{
            form:{
                name: '',
                email: '',
                password:'',
                password_confirmation:'',
            },
            errors:[]
        }
    },
        validations: {
            user: {
                name: { required },
                email: { required, email },
                password: { required, minLength: minLength(6) },
                password_confirmation: { required, sameAsPassword: sameAs('password') },
                
                
            }
        },
    methods:{
        saveForm(){
            axios.post('/api/register', this.form).then(() =>{
                console.log('saved');
                document.querySelector(".text-red-500").style.display = "none";
                document.querySelector(".text-green-500").style.display = "block";
                
            }).catch((error) =>{
                this.errors = error.response.data.errors;
            })
        }
    }
}
</script>