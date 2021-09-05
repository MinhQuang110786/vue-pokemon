<template>
    <div class="screen">
        <div class="screen_inner">
            <h1>✨✨ Congratulation ✨✨</h1>
            <p>{{getSeconds}} seconds</p>
            <button @click="onStartAgain">Start again</button>
        </div>
        
    </div>
</template>

<script>
    export default {
        name:"ResultScreen",
        props:{
            timer:{
                type:Number,
                required:true
            }
        },
        computed:{
            getSeconds(){
                return Math.floor(this.timer/1000);
            }
        },
        methods:{
            onStartAgain(){
                this.$emit("startAgain");
            }
        }
    }
</script>

<style scoped>
    .screen{
        width: 100%;
        height: 100vh;
        position: absolute;
        top:0;
        left:0;
        background: var(--dark);
        color:var(--light);
        font-family: var(--font);
    }
    .screen_inner{
        position: fixed;
        top: 50%;
        left:50%;
        transform: translate(-50%,-50%);
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        font-size: 1.5rem;
    }
    .screen_inner h1{
        font-size: 3rem;
        margin-bottom: 1rem;
    }
    .screen p{
        margin-bottom: 1rem;
    }
    .screen button{
        background: var(--dark);
        color: var(--light);
        width: 100px;
        height: 40px;
        border: 1px solid var(--light);
        border-radius: 1.2rem;
        font-family: inherit;
        cursor: pointer;
        transition: 1000ms;
    }
    .screen button:hover{
        background: var(--light);
        color: var(--dark);

    }
</style>