<template>
    <div class="w-25">
        <input type="email" v-model="email" class="form-control mb-3" placeholder="email">
        <input type="password" v-model="password" class="form-control mb-3" placeholder="password">
        <input @click.prevent="login" type="submit" class="btn btn-success mb-3" value="submit">
    </div>
</template>

<script>
    export default {
        name: "Login",
        data: () => ({
            email: null,
            password: null,
        }),
        methods: {
            login(){
                axios.get('/sanctum/csrf-cookie').then(res => {
                    axios.post('/login', {email: this.email, password: this.password}).then(response => {
                        localStorage.setItem("x_xsrf", response.config.headers["X-XSRF-TOKEN"])
                        this.$router.push({name: 'user.personal'})
                    })
                    .catch(err => {
                        console.log(err.response)
                    })
                })

            }
        }
    }
</script>

<style scoped>

</style>
