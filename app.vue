<template>
  <main>
    <p 
      class="diff-time undisplay"
      :class="{ 'display' : isDisplay }"
    >
      {{ diffTime }}
    </p>
    <button @click="toggle">START</button>
  </main>
</template>

<script>
export default {
  data() {
    return {
      isRunning: false,
      isDisplay: true,
      nowTime: 0,
      startTime: 0,
      diffTime: 0,
      timerId: '',
    }
  },
  methods: {
    toggle(){
      if (this.isRunning) {
        this.stop();
      } else {
        this.start();
      }
    },
    start() {
      this.isRunning = true;
      this.startTime = new Date();

      if (this.isRunning){
        this.timerId = setInterval(() => {
          this.nowTime = new Date();
          this.diffTime = ((this.nowTime - this.startTime) / 1000).toFixed(2);

          if (this.diffTime >5){
            this.isDisplay = false;
          }
        },10)
      }
    },
    stop() {
      this.isRunning = false;
      clearInterval(this.timerId);
      this.isDisplay = true;
    }
  },
}
</script>

<style lang="scss" scoped>
main{
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  height: 100vh;
}
button{
  width: 100px;
  height: 100px;
  border-radius: 50%;
  border: none;
  background: #54C4C4;
  color: white;
  font-size: 16px;
}
.diff-time{
  font-size: 64px;
  font-family:Arial, Helvetica, sans-serif
}
.undisplay{
  opacity: 0;
  transition: 1s opacity;
}
.display{
  transition: none;
  opacity: 1;
}
</style>
