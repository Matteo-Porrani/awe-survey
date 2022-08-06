<template>
    <section class="my-3">
        <div class="container">
            <div class="row">
                <div class="col border border-secondary">
                    <div id="progressBar" class="div" :style="progressWidth"></div>
                    <p>Question {{ counter }}/{{ total }}</p>
                </div>
            </div>
        </div>
    </section>
</template>

<script>

export default {
    name: "ProgressBar",
    props: {
        total: {
            type: Number,
            required: true,
        },
        counter: {
            type: Number,
            required: true,
        }
    },
    computed: {
        progressWidth() {
            return 'width: ' + ((this.counter * 100) / this.total) + '%;';
        }
    }
}
</script>

<style scoped>
    #progressBar {
        height: 10px;
        background-color: #15d;
    }
</style>