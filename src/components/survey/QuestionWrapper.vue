<template>

    <ProgressBar :counter="id" total="3"/>
    <section class="py-3">
        <div class="container">
            <p>{{ }}</p>
            <h4 class="fw-bold text-center">{{ question.question }}</h4>
        </div>
    </section>


    <section class="py-3 mt-3">
        <div class="container">
            <div v-for="(ans, idx) in question.answers" :key="idx" class="text-center">
                <div @click="selectAnswer" :data-ref="idx"
                     class="option-btn btn btn-outline-dark m-2">{{ ans }}
                </div>
            </div>
        </div>
    </section>


    <section class="py-3 mt-3 text-center">
        <div class="container">
            <button @click="moveToNextQuestion" class="btn btn-warning m-2">Confirmer ma réponse</button>
        </div>
    </section>
</template>

<script>
import ProgressBar from './ProgressBar.vue';

export default {
    name: "QuestionWrapper",
    components: {
        ProgressBar,
    },
    props: {
        id: {
            type: Number,
            required: true,
        },
        question: {
            type: Object,
            required: true,
        }
    },
    data() {
        return {
            selectedAnswer: null,
        }
    },
    methods: {
        moveToNextQuestion() {
            this.$emit('confirm', this.selectedAnswer);
            this.selectedAnswer = null;
            this.resetAnswers();
        },
        selectAnswer(e) {
            console.log(e.target.dataset.ref);
            this.selectedAnswer = e.target.dataset.ref;

            const options = document.querySelectorAll('.option-btn');
            options.forEach(opt => {
                if (opt.dataset.ref === this.selectedAnswer) {
                    opt.classList.add('btn-danger');
                    opt.classList.add('fw-bold');
                    opt.classList.remove('btn-outline-dark');
                    opt.classList.remove('btn-outline-secondary');
                } else {
                    opt.classList.remove('btn-danger');
                    opt.classList.remove('fw-bold');
                    opt.classList.remove('btn-outline-dark');
                    opt.classList.add('btn-outline-secondary');
                }
            });
        },
        resetAnswers() {
            const options = document.querySelectorAll('.option-btn');
            options.forEach(opt => {
                opt.className = 'option-btn btn btn-outline-dark m-2';
            });
        }
    }
}
</script>

<style scoped>

</style>