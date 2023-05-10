<script>
import card from "./Card.vue";

export default {
    props: {
        cardContexts: {
            type: Array,
            default: []
        },
    },
    components: {
        card,
    },
    methods: {
        checkRules(event) {
            if (this.rules.length === 2) this.rules = [];
            this.rules.push(event);
            if (this.rules.length === 2 &&
                this.rules[0].card === this.rules[1].card &&
                this.rules[0].index !== this.rules[1].index) {
                this.$refs.cards[this.rules[0].index].onDisable();
                this.$refs.cards[this.rules[1].index].onDisable();
                this.countToWin++;
                console.log(this.countToWin);
                if (this.countToWin === this.cardContexts.length / 2) {
                    let endTime = new Date().getTime();
                    this.$emit('onWin', endTime);
                }
            } else if (this.rules.length === 2 &&
                this.rules[0].card !== this.rules[1].card) {
                setTimeout(() => {
                    this.$refs.cards[this.rules[0].index].onClosedCard();
                    this.$refs.cards[this.rules[1].index].onClosedCard();
                }, 1000);
            } else {
                return false;
            }
        },

    },
    data() {
        return {
            rules: [],
            countToWin: 0,
            UIFlag : 0
        }
    },
    mounted() {
            if (this.cardContexts.length === 16) this.UIFlag = 16;
            if (this.cardContexts.length === 36) this.UIFlag = 36;
            if (this.cardContexts.length === 64) this.UIFlag = 64;
            if (this.cardContexts.length === 100) this.UIFlag = 100;
    }

}
</script>

<template>
    <div class="interact"
         :class="{
            'interact--36' : UIFlag === 36,
            'interact--64' : UIFlag === 64,
            'interact--100' : UIFlag === 100,
            }"
    >
        <div class="interact__inner" :class="{
            'interact__inner--36' : UIFlag === 36,
            'interact__inner--64' : UIFlag === 64,
            'interact__inner--100' : UIFlag === 100,
            }">
            <card v-for="(card,index) in this.cardContexts "
                  :key="index"
                  :backgroundImage="`${card}.png`"
                  :card="{card : card , index : index}"
                  @onFlipped="checkRules($event)"
                  ref="cards"
                  :class="{
                        'card--36' : UIFlag === 36,
                        'card--64' : UIFlag === 64,
                        'card--100' : UIFlag === 100,
                        }"
            >
            </card>
        </div>
    </div>
</template>

<style scoped>
.interact {
    width: 100%;
    height: 100vh;
    position: absolute;
    top: 0;
    left: 0;
    z-index: 2;
    background-color: #363232;
    color: var(--light);
}
.interact__inner {
    width: 544px;
    display: flex;
    flex-wrap: wrap;
    margin: 120px auto;
}

.interact--36 {
    height: auto;
}
.interact--64 {
    height: auto;
}
.interact--100 {
    height: auto;
}
.interact__inner--36 {
    width: 816px;
    margin: 0 auto;
}
.interact__inner--64 {
    width: 850px;
    margin: 0 auto;
}
.interact__inner--100 {
    width: 1150px;
    margin: 0 auto;
}

.card--36 {
    width: 120px;
    height: 146.8px;
}
.card--64 {
    width: 82px;
    height: 97px;
}
.card--100 {
    width: 90px;
    height: 81.7px;
}
</style>