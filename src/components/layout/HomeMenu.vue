<template>
    <section class="border">
        <div class="container">
            <div class="row text-center">
                <div class="col-12 col-md-6 my-3">
                    <button @click="$emit('start')" class="btn btn-warning py-3 w-75">Participer au sondage</button>
                </div>
                <div class="col-12 col-md-6 my-3">
                    <button class="btn btn-success py-3 w-75">Voir les résultats</button>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
export default {
    name: "HomeMenu",
}
</script>

<style scoped>

</style>