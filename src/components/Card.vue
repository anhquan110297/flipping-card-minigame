<script>
export default {
    props: {
        backgroundImage: {
            type: String,
            required: true
        },
        card: {
            type: [String, Number, Object, Array],
            required: true
        }
    },
    data() {
        return {
            isFlipped: false,
            isDisable: false
        }
    },
    methods: {
        onToggleFlipCard() {
            if (!this.isDisable) {
                this.isFlipped = !this.isFlipped;
                if (this.isFlipped) this.$emit('onFlipped', this.card);
            }
        },
        onClosedCard() {
            this.isFlipped = false;
        },
        onDisable() {
            this.isDisable = true;
        }
    }
}
</script>

<template>
    <div class="card">
        <div class="card__wrapper"
             :class="{ 'is-flipped' : isFlipped , 'is-disable' : isDisable}"
             @click="onToggleFlipCard">
            <div class="card__face card__face--front">
                <div class="card__content">
                </div>
            </div>
            <div class="card__face card__face--back">
                <div class="card__content"
                     :style="{ 'backgroundImage' :  `url('../src/assets/images/${this.backgroundImage}')`}">
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
template {
    background-color: #ffce00;
}

.card {
    display: inline-block;
    margin-right: 1rem;
    margin-bottom: 1rem;
    width: 120px;
    height: 160px;
}

.card__wrapper {
    /*
     XAC DINH GOC TOA DO
     neu khong xac dinh goc toa do thi khi xoay se tro ve goc man hinh
     */
    position: relative;
    width: 100%;
    height: 100%;
    transform-style: preserve-3d;
    transition: transform 1s;
    cursor: pointer;
}

.card__wrapper.is-flipped {
    transform: rotateY(-180deg);
}

.card__wrapper.is-disable {
    cursor: default;
}

.card__face {
    position: absolute;
    width: 100%;
    height: 100%;
    -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
    overflow: hidden;
    border-radius: 1rem;
    padding: 1rem;
    box-shadow: 0 3px 18px 3px rgba(0,0,0,.2);
}

.card__face--front .card__content {
    background: url("../assets/images/icon_back.png") no-repeat center center;
    background-size: 40px 40px;
    height: 100%;
    width: 100%;
}

.card__face--back {
    transform: rotateY(-180deg);
    background-color: var(--light);
}

.card__face--back .card__content {
    height: 100%;
    width: 100%;
    background-size: contain;
    background-position: center center;
    background-repeat: no-repeat;
}
</style>