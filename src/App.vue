<template>
    <TheHeader :step="currentStep"/>
    <p class="text-center">
        <span class="badge bg-danger">{{ phase }}</span>
    </p>
    <p class="text-center">
        <span class="badge bg-info">{{ currentQuestion }}</span>
    </p>
    <TheFlag v-if="currentStep < 1"/>
    <HomeMenu @start="moveOneStep" v-if="currentStep < 1"/>
    <UserRegistration @register="registerUser" v-if="(currentStep === 1)"/>

    <QuestionWrapper v-if="(phase === 'survey')" @confirm="storeAnswer" :id="currentQuestion" :question="questions[currentQuestion]"/>
    <GoodbyeMessage v-if="(phase === 'goodbye')"/>


</template>

<script>
import seedsQuestions from "@/seeds/questions.js";
import TheHeader from "@/components/layout/TheHeader.vue";
import TheFlag from "@/components/layout/TheFlag.vue";
import HomeMenu from "@/components/layout/HomeMenu.vue";
import UserRegistration from "@/components/layout/UserRegistration.vue";
import QuestionWrapper from "@/components/survey/QuestionWrapper";
import GoodbyeMessage from "@/components/layout/GoodbyeMessage";

export default {
    name: 'App',
    components: {
        TheHeader,
        TheFlag,
        HomeMenu,
        UserRegistration,
        QuestionWrapper,
        GoodbyeMessage,

    },
    data() {
        return {
            questions: seedsQuestions,
            currentStep: 0,
            currentQuestion: 1,
            phase: 'intro',
            opinion: {
                user: null,
                datetime: null,
                answers: []
            },
        }
    },
    methods: {
        moveOneStep() {
            this.currentStep++;
        },
        storeAnswer(choice) {
            this.opinion.answers.push(choice)
            if (this.currentQuestion < 3) {
                this.currentQuestion++;
            } else {
                this.phase = 'goodbye';
            }

            console.log(this.opinion.answers);
        },
        registerUser(username) {
            this.opinion.user = username;
            this.moveOneStep();
        },
        sendDataToAPI(data) {
            fetch('https://doctypematt.alwaysdata.net/api/opinion', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify(data)
            });
        }
    },
    watch: {
        currentStep(newValue) {
            if (newValue > 1) {
                this.phase = 'survey';
                console.log(('survey'));
            }
        },
        phase(newValue) {
            if (newValue === 'goodbye') {
                this.opinion.datetime = new Date().toISOString();


                // FIXME -- reactivate sendData...
                // this.sendDataToAPI(this.opinion);
                console.log(this.opinion);
            }
        }
    },
    mounted() {
        // console.log(this.questions);
    }
}
</script>

<style lang="scss">
#app {
    font-family: 'Exo 2', sans-serif;
}

#mgpLogo {
    width: 250px;
}
</style>
