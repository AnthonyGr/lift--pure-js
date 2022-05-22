<template>
  <div class="container">
    <h1 class="header">L I F T</h1>
    <FloorsList
      v-bind:floors="floors"
      v-bind:queue="queue"
      v-bind:direction="direction"
      v-bind:position="position"
      @handle-click="handleClick"
    />
  </div>
</template>

<script>
import FloorsList from "./components/FloorsList.vue";
export default {
  name: "App",
  data() {
    return {
      position: 0,
      direction: "stay",
      currentFloor: 1,
      step: 102,
      doorsOpen: true,
      floors: [
        { id: 5, title: 5, isDisabled: false },
        { id: 4, title: 4, isDisabled: false },
        { id: 3, title: 3, isDisabled: false },
        { id: 2, title: 2, isDisabled: false },
        { id: 1, title: 1, isDisabled: true },
      ],
      queue: [],
    };
  },
  methods: {
    handleClick(id) {
      this.floors.find((btn) => btn.id === id).isDisabled = true;
      this.queue.push(id);
      this.queue.push(1);
      if (this.direction === "stay") {
        this.liftLoop();
      }
    },
    async animStep() {
      console.log("start");

      if (this.direction === "down") {
        this.position = this.position + 2;
        if (this.position < -(this.queue[0] - 1) * this.step) {
          requestAnimationFrame(this.animStep);
        } else {
          this.direction = "stay";
          this.currentFloor = this.queue[0];
          this.queue.splice(0, 1);
          await this.sleep(500);
          this.activateBtn();
          this.liftLoop();
        }
      } else if (this.direction === "up") {
        this.position = this.position - 2;
        if (-this.position < (this.queue[0] - 1) * this.step) {
          requestAnimationFrame(this.animStep);
        } else {
          this.direction = "stay";
          this.currentFloor = this.queue[0];
          this.queue.splice(0, 1);
          await this.sleep(500);
          this.activateBtn();
          this.liftLoop();
        }
      }
    },
    moveLift() {
      requestAnimationFrame(this.animStep);
    },
    liftLoop() {
      if (this.currentFloor < this.queue[0]) {
        this.direction = "up";
        this.moveLift();
        console.log("here");
      }

      if (this.currentFloor > this.queue[0]) {
        this.direction = "down";

        if (this.queue[1] < this.currentFloor) {
          this.queue.splice(0, 1);
        }
        this.moveLift();
      }

      if (!this.queue[0]) {
        this.direction = "stay";
      }
    },
    activateBtn() {
      if (this.currentFloor !== 1) {
        this.floors.find(
          (btn) => btn.id === this.currentFloor
        ).isDisabled = false;
      }
    },
    sleep(ms) {
      return new Promise((r) => setTimeout(r, ms));
    },
    // animate(options) {
    //   const duration = 1000;
    //   var start = performance.now();
    //   requestAnimationFrame(function animate(time) {
    //     // timeFraction от 0 до 1
    //     var timeFraction = (time - start) / duration;
    //     if (timeFraction > 1) timeFraction = 1;
    //     // текущее состояние анимации
    //     var progress = options.timing(timeFraction);

    //     options.draw(progress);

    //     if (timeFraction < 1) {
    //       requestAnimationFrame(animate);
    //     }
    //   });
    // },
  },
  components: {
    FloorsList,
  },
};
</script>

<style>
#app {
}

body {
  font-family: "Roboto", "Arial", sans-serif;
  text-align: center;
  margin: 20px 0;
  padding: 0;
  height: 100%;
  width: 100%;
  background-color: rgb(53, 68, 76);
  box-sizing: content-box;
}

.container {
  max-width: 320px;
  margin: 0 auto;
}

.header {
  margin: 10px 0;
  font-size: 40px;
  line-height: 1.2;
  color: #fff;
  text-align: center;
}
</style>
