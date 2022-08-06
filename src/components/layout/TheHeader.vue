<template>
    <header>
        <section class="bg-dark text-center text-light py-4">
            <img id="mgpLogo" src="../../assets/logo2.svg" alt="mgpbattle logo">
            <p class="fw-bold my-1">
                <span class="badge bg-danger">{{ step }}</span>
            </p>
        </section>
        <section class="bg-warning py-2 text-center">
            <h5 class="fw-bold">Le sondage des champions</h5>
        </section>
    </header>
</template>

<script>
export default {
    name: "TheHeader",
    props: {
        step: {
            type: Number,
            required: true,
        }
    }
}
</script>

<style scoped>

</style>