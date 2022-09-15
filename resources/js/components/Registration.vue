<template>
    <div class="w-25">
        <input type="text" v-model="name" class="form-control mb-3" placeholder="name">
        <input type="email" v-model="email" class="form-control mb-3" placeholder="email">
        <input type="password" v-model="password" class="form-control mb-3" placeholder="password">
        <input type="password" v-model="password_confirmation" class="form-control mb-3" placeholder="confirmation_password">
        <input @click.prevent="register" type="submit" class="btn btn-success" value="submit">
    </div>
</template>

<script>
    export default {
        name: "Registration",
        data: () => ({
            name: null,
            email: null,
            password: null,
            password_confirmation: null,
        }),
        methods: {
            register(){
                axios.get('/sanctum/csrf-cookie').then(res => {
                    axios.post('/register', {
                        email: this.email,
                        name: this.name,
                        password: this.password,
                        password_confirmation: this.password_confirmation}).then(response => {
                        localStorage.setItem("x_xsrf", response.config.headers["X-XSRF-TOKEN"])
                        this.$router.push({name: 'user.personal'})
                    })
                })
            }
        }
    }
</script>

<style scoped>

</style>
