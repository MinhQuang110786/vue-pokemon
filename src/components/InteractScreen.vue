<template>
<div class="screen">
    <div class="screen_inner" :style="{'grid-template-columns':`repeat(${this.matrixSize},1fr)`,
                  'grid-template-rows':`repeat(${this.matrixSize},1fr)`      
                }">
        <card-flip v-for="(card,index) in cardsContext" :key="index" :size="matrixSize" :ref="`card-${index}`" :imgBackFaceUrl="`images/${card}.png`" :card="{index,value:card}" @onFlip="checkRule($event)" />
    </div>

</div>
</template>

<script>
import CardFlip from "./Card.vue"
export default {
    name: "InteractScreen",
    data() {
        return {
            rules: [],
            right: 0
        }
    },
    props: {
        cardsContext: {
            type: Array,
            default: function () {
                return [];
            }
        }
    },
    components: {
        CardFlip,

    },
    computed: {
        matrixSize() {
            return Math.floor(Math.sqrt(this.cardsContext.length));
        }
    },
    methods: {
        checkRule(card) {
            if (this.rules.length == 2)
                return false;
            this.rules.push(card);
            if (this.rules.length === 2 && this.rules[0].value === this.rules[1].value) {
                if (this.rules[0].index !== this.rules[1].index) {
                    this.$refs[`card-${this.rules[0].index}`].onEnableDisableMode()
                    this.$refs[`card-${this.rules[1].index}`].onEnableDisableMode()
                    this.rules = []
                    this.right++;

                    if (this.right === this.cardsContext.length / 2) {
                        setTimeout(() => {
                            this.$emit("onFinish")
                        }, 1000)
                    }
                } else {
                    this.rules = [this.rules[0]];
                }

            } else if (this.rules.length === 2 && this.rules[0].value !== this.rules[1].value) {
                console.log("Wrong")

                setTimeout(() => {
                    this.$refs[`card-${this.rules[0].index}`].onFlipBackCard()
                    this.$refs[`card-${this.rules[1].index}`].onFlipBackCard()
                    this.rules = []
                }, 800)

            } else return false;
        }
    }
}
</script>

<style scoped>
.screen {
    width: 100%;
    height: 100vh;
    position: absolute;
    top: 0;
    left: 0;
    z-index: -1;
    background: var(--dark);
    color: var(--light);
}

.screen_inner {
    width: 1200px;
    display: grid;
    margin: 1.2rem auto;
}
</style>
