<template>

    <ProgressBar :counter="parseInt(id) - 1" total="3"/>

    <div>
        <section id="questionHeader" class="py-3">
            <div class="container">
                <p>{{ }}</p>
                <h5 class="fw-bold text-center">{{ question.question }}</h5>
            </div>
        </section>


        <section id="questionAnswers" class="py-3 mt-3">
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
            return idx == this.selectedAnswer ? 'btn-primary fs-5 fw-bold' : 'btn-outline-dark';
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

    #questionHeader {
        animation: questionIn .6s ease-out;
    }

    #questionAnswers {
        opacity: 0;
        animation: answersIn 1s .6s ease-out forwards;
    }

    @keyframes questionIn {
        0% {
            transform: translateY(20px);
            opacity: 0;
        }
        100% {
            transform: translateY(0px);
            opacity: 1;
        }
    }

    @keyframes answersIn {
        0% {
            opacity: 0;
        }
        100% {
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