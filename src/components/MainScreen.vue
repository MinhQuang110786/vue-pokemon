<template>
  <div class="screen">
    <h1>POKE MEMORIES</h1>
    <h3>Select mode to start game</h3>
    <div class="action">
      <button @click="onStart(16)">
        <span>4x4</span>
        <span>Easy</span>
      </button>
      <button @click="onStart(36)">
        <span>6x6</span>
        <span>Normal</span>
      </button>
      <button @click="onStart(64)">
        <span>8x8</span>
        <span>Hard</span>
      </button>
      <button @click="onStart(100)">
        <span>10x10</span>
        <span>World class</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
    name:'MainScreen',
    methods:{
        onStart(totalOfBlocks){
            this.$emit("onStart",{totalOfBlocks})
        }
    }
};
</script>

<style scoped>
  .screen{
    position: absolute;
    top:50%;
    left:50%;
    transform: translate(-50%,-50%);
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100vh;
    background: var(--dark);
    color: var(--light);
  }
  .screen h1{
    font-size: 2.5rem;
  }
  .action{
    display: flex;
  }
  .action button{
    flex: 1;
    margin: 1rem;
    display:flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    cursor:pointer;
    border: 1px solid var(--light);
    width: 90px;
    height: 90px;
    background: var(--dark);
    border-radius: 0.5rem;
    transition: ease-in-out;
  }
  .action button span{
    font-family: var(--font);
    color: var(--light);
    font-size: 1.2rem;
    
  }
  .action button:hover{
    background: var(--light);
    color: var(--dark);
  }
   .action button:hover span{
     font-family: var(--font);
    color: var(--dark);
    font-size: 1.2rem;
   }
</style>
