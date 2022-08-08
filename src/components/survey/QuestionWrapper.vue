<template>

    <ProgressBar :counter="parseInt(id) - 1" total="3"/>

    <div id="questionBody">
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
                         class="answer-btn btn m-2"
                         :class="getAnswerBtnClass(idx)"
                    >{{ ans }}
                    </div>

                </div>
            </div>
        </section>


        <section
            class="py-3 mt-3 text-center">
            <div class="container">
                <button v-if="selectedAnswer != null"
                        @click="moveToNextQuestion"
                        class="btn btn-warning m-2"
                >Confirmer ma réponse
                </button>
            </div>
        </section>
    </div>
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
    computed: {},
    methods: {
        getAnswerBtnClass(idx) {
            return idx == this.selectedAnswer ? 'btn-primary fs-4' : 'btn-outline-dark';
        },
        moveToNextQuestion() {
            this.$emit('confirm', this.selectedAnswer);
            this.selectedAnswer = null;
            this.resetAnswers();
        },
        selectAnswer(e) {
            console.log(e.target.dataset.ref);
            this.selectedAnswer = e.target.dataset.ref;
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
    .answer-btn {
        transition: all .3s ease-out;
    }

    #questionBody {
        animation: questionIntro .6s ease-out;
    }

    @keyframes questionIntro {
        0% {
            transform: translateY(30px);
            opacity: 0;
        }
        100% {
            transform: translateY(0px);
            opacity: 1;
        }
    }

    button {
        animation: buttonIn .3s ease-out;
    }

    @keyframes buttonIn {
        0% {
            transform: scale(.9);
            opacity: 0;
        }
        100% {
            transform: scale(1);
            opacity: 1;
        }
    }
</style>