<template>
    <div class="card" :class="{disabled:isDisabled}"
        :style="{'width':`${getSize.width}px`,
                 'height':`${getSize.height}px`,
                 'perpective':`${getSize.width*2}px`
                }"    
    >
        <div class="card_inner" :class="{'is-flipped': isFlipped}" @click="onToggleFlipCard">
            <div class="card_face card_face--front">
                <div class="card_content"></div>
            </div>
            <div class="card_face card_face--back">
                <div class="card_content" 
                    :style="{backgroundImage:`url(${require('@/assets/'+ imgBackFaceUrl)})`}">
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name:"Card",
        data(){
            return{
                isFlipped:false,
                isDisabled:false
            }
        },
        props:{
            imgBackFaceUrl:{
                type:String,
                required:true
            },
            card:{
                type:[String,Number,Array,Object]
            },
            size:{
                type:Number,
                required:true
            }
        },
        computed:{
            getSize(){
                return{
                    width: Math.floor(540/this.size),
                    height: Math.floor(720/this.size)
                }
            }
        },
        methods:{
            onToggleFlipCard(){
                if(this.isDisabled)
                    return false;
                this.isFlipped = !this.isFlipped
                if(this.isFlipped)
                    this.$emit("onFlip",this.card)
            },
            onFlipBackCard(){
                this.isFlipped = false
            },
            onEnableDisableMode(){
                this.isDisabled = true
            }
        }
    }
</script>

<style scoped>
 .card{
     display:block;
     margin-bottom: 1rem;
 }
 .card_inner{
     width:100%;
     height:100%;
     transition: transform 1s;
     transform-style: preserve-3d;
     cursor: pointer;
     position: relative;
 }
 .card_inner.is-flipped{
     transform: rotateY(-180deg);
 }
 .card_face {
     position:absolute;
     width: 100%;
     height:100%;
     backface-visibility: hidden;
     overflow: hidden;
     border-radius: 1rem;
     padding:0.8rem;
     box-shadow: 0 3px 10px 3px rgba(0,0,0,0.2);
 }

 .card_face--front .card_content{
     background: url("../assets/images/icon_back.png") no-repeat center;
     background-size: 40px 40px;
     height: 100%;
     width: 100%;
 }
 .card_face--back{
     background-color: var(--light);
     transform: rotateY(-180deg);
 }

 .card_face--back .card_content{
     background-size: contain;
     background-position: center center;
     background-repeat: no-repeat;
     height: 100%;
     width: 100%;   
 }

 .card.disabled .card_inner{
     cursor: default;
 }
</style>