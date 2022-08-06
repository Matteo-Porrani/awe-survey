<template>
    <section class="my-5 text-center">
        <div class="container">
            <form @submit.prevent="sendUsername">
                <div class="row">
                    <div class="col">
                        <label class="form-label">Insérer votre nom</label>
                        <input v-model="username" class="form-control text-center" type="text">
                    </div>
                </div>
                <div class="row mt-5">
                    <div class="col">
                        <button class="btn btn-warning">Commencer</button>
                    </div>
                </div>
            </form>
        </div>
    </section>
</template>

<script>
export default {
    name: "UserRegistration",
    data() {
        return {
            username: '',
        }
    },
    methods: {
        sendUsername() {
            this.$emit('register', this.username);
        }
    }
}
</script>

<style scoped>

</style>