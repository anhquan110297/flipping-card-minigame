<script>
import MainScreen from "./components/MainScreen.vue"
import ResultScreen from "./components/ResultScreen.vue"
import InteractScreen from "./components/InteractScreen.vue"

export default {
    name: "App",
    components: {
        MainScreen,
        ResultScreen,
        InteractScreen
    },
    data() {
        return {
            settings: {
                numberOfBlocks: 0,
                cardContexts: [],
            },
            statusMatch: 'beforeMatch',
            startTime : 0,
            endTime : 0,

        }
    },

    methods: {
        onChangeStatusMatch(event) {
            this.settings.totalOfBlocks = event.numberOfBlocks;
            let arr = [];
            while (arr.length < this.settings.totalOfBlocks / 2) {
                const randomNum = Math.floor(Math.random() * 64) + 1;
                if (!arr.includes(randomNum)) {
                    arr.push(randomNum);
                }
            }
            this.settings.cardContexts = [...arr, ...arr].sort(() => Math.random() - 0.5);
            this.startTime = event.startTime;
            this.statusMatch = 'start';
        },
        onHandleWin(event) {
            this.endTime = event;
            this.statusMatch = 'win';
        }
    }
}
</script>

<template>
    <main-screen
            v-if="statusMatch === 'beforeMatch'"
            @onStartGame="onChangeStatusMatch($event)"
    />
    <interact-screen
            v-if="statusMatch === 'start'"
            :cardContexts="this.settings.cardContexts"
            @onWin="onHandleWin($event)"
    >
    </interact-screen>
    <result-screen
            v-if="statusMatch === 'win'"
            :startTime="this.startTime"
            :endTime="this.endTime"
    >
    </result-screen>
</template>

<style scoped>

</style>
