<template>
  <div
    class="lift"
    :style="style"
    :class="{ 'doors-open': direction === 'stay' }"
  ></div>
</template>

<script>
export default {
  props: ["position", "direction"],
  computed: {
    style() {
      return { transform: "translateY(" + this.position + "px)" };
    },
  },
};
</script>

<style scoped>
.lift {
  width: 100px;
  height: 100px;
  background: url("../assets/lift.png");
  background-repeat: no-repeat;
  background-position: center;
  background-size: 100%;
  border: 1px solid green;
  position: absolute;
  /* bottom: 20px; */
}

.doors-open {
  background-image: url("../assets/lift-open.png");
}
</style>
