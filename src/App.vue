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
  background-image: url("../img/sea.jpg");
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
  width: 100%;
  height: 100%;
  text-align: center;
}

.container{
  max-width: 3000px;
  margin: 0 auto;
  padding: 15px 0;
}

</style>
