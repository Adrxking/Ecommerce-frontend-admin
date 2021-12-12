<template>
    <div>
        <h3>Account Information</h3>
        <form @submit.prevent="infoSubmit">
            <div class="mb-3">
                <v-text-field label="First Name" v-model="user.first_name" />
            </div>
            <div class="mb-3">
                <v-text-field label="Last Name" v-model="user.last_name" />
            </div>
            <div class="mb-3">
                <v-text-field label="Email" type="email" v-model="user.email" />
            </div>
            <v-btn color="primary" type="submit">Submit</v-btn>
        </form>

        <h3 class="mt-4">Change password</h3>
        <form @submit.prevent="passwordSubmit">
            <div class="mb-3">
                <v-text-field label="Paswword" v-model="password" />
            </div>
            <div class="mb-3">
                <v-text-field label="Paswword Confirm" v-model="password_confirm" />
            </div>
            <v-btn color="primary" type="submit">Submit</v-btn>
        </form>
    </div>
</template>

<script>
import axios from "axios";

export default {
    name: "Profile",
    data() {
        return {
            password: '',
            password_confirm: '',
        }
    },
    methods: {
        async infoSubmit() {
            await axios.put('users/info', {
                first_name: this.user.first_name,
                last_name: this.user.last_name,
                email: this.user.email,
            })
        },
        async passowrdSubmit() {
            await axios.put('users/password', {
                password: this.password,
                password_confirm: this.password_confirm,
            })
        }
    },     
    computed: {
        user() {
        return this.$store.state.user;
        }
    }
}
</script>