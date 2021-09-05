<template>
    <div class="copyright">
        <p>
            This game is created by Quang Minh - <a href="#">view here</a>
        </p>
    </div>
    
</template>

<script>
    export default {
        name:"CopyRightScreen"
    }
</script>

<style scoped>
    .copyright{
        position: fixed;
        left:50%;
        transform: translateX(-50%);
        bottom: 1.5rem;
    }
   .copyright p{
        color: var(--light);
        font-family: var(--font);
        font-size: 1.2rem;
   }
   .copyright p a{
       text-decoration: none;
       color: yellow;
   }
   
</style>