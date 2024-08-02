<script>
import Canvas from './components/Canvas.vue'

export default {
	components: {
    Canvas
	}
}
</script>

<template>
  <main>
    <Canvas></Canvas>
  </main>
  
</template>

<style scoped>
  main{
    height: 100vh;
    width: 100vw;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

</style>
