<script setup>
import TheTimer from "./components/TheTimer.vue"

</script>

<template>
    <div class="wrapper">
        <TheTimer></TheTimer>        
    </div>
</template>

<style>
.wrapper {
  max-width: 1600px;
  background-image: url("../img/love3Bg.avif");
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
  width: 100%;
  height: 100vh;
  text-align: center;
  opacity: 0.9;
}

.container{
  max-width: 1300px;
  margin: 0 auto;
  padding: 15px 0;
}

</style>
