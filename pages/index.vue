<script>
export default {
    setup() {
        definePageMeta({
            middleware: 'auth'
        });
    },
    data() {
        return {
            user: {}
        }
    },
    async mounted() {
        const { data } = await useAuth();
        this.user = data.value.user;
    },
    methods: {
        async handleLogout() {
            const { signOut } = await useAuth();

            await signOut();
        }
    }
}
</script>

<template>
    <div>
        <h1 class="mb-4 text-xl font-bold">Welcome {{ user.username }}</h1>
        <p>Access your dashboard and account from here</p>

        <button type="button" class="bg-red-500 hover:bg-red-600 transition-all duration-200 text-red-50 rounded-lg py-2 px-5 mt-4" @click="handleLogout">
            Logout
        </button>
    </div>
</template>