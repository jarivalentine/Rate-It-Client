
<template >
    <main class="login">
        <section>
            <h1>RATE-IT</h1>

            <h2>
                Random meme for you
            </h2>

            <meme></meme>
            <!-- TODO INSER RANDOM MEME -->
        </section>

        <aside>

            <h2>Sign in</h2>
            <form @submit.prevent method="post">
                <input type="text" placeholder="e-mail" v-model="email">

                <input type="password" placeholder="password" name="pw" id="pw" v-model="password">

                <button @click="login" type="submit">Login</button>
            </form>
            <p>Don't have an account? <RouterLink class="link" to="/register">Create Acount</RouterLink>
            </p>

        </aside>

    </main>
</template>
<script>
import { RouterLink, useRouter } from 'vue-router';
import Meme from '../modules/Meme/components/Meme.vue';
import AuthService from '../modules/Auth/services/AuthService';
export default {
    name: 'LoginView',
    components: {
        RouterLink,
        Meme
    },
    data() {
        return {
            "service": new AuthService(),
            router: new useRouter(),
            email: "",
            password: ""
        }
    },
    methods: {
        async login() {
            const res = await this.service.login(this.email, this.password)
            if (!res) {
                alert("Wrong email or password")
            } else {
                this.router.push({ name: 'home', params: { lang: 'nl' } })
            }
        }
    },
}
</script>