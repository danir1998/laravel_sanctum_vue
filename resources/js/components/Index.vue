<template>
    <div>
        <router-link v-if="token" :to="{ name: 'get.index'}">get</router-link>
        <router-link v-if="!token" :to="{ name: 'user.login'}">login</router-link>
        <router-link v-if="!token" :to="{ name: 'user.registration'}">registration</router-link>
        <router-link v-if="token" :to="{ name: 'user.personal'}">Personal</router-link>
        <a v-if="token" @click.prevent="logout" href="#">Logout</a>
        <router-view></router-view>
    </div>
</template>

<script>
    export default {
        name: "Index",
        data: () => ({
            token: null
        }),
        mounted() {
            this.getToken();
        },
        updated() {
            this.getToken();
        },
        methods: {
            getToken() {
                this.token = localStorage.getItem("x_xsrf")
            },
            logout(){
                axios.post('/logout').then(res => {
                    localStorage.removeItem("x_xsrf");
                    this.$router.push({name: 'user.login'})
                })
            }
        }
    }
</script>

<style scoped>

</style>
