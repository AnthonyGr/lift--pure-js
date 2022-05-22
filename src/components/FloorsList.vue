<template>
  <main class="main">
    <CallQueue v-bind:queue="queue" />
    <div class="floors">
      <FloorsItem
        v-for="floor of floors"
        v-bind:key="floor.id"
        v-bind:floor="floor"
        v-bind:position="position"
        v-bind:direction="direction"
        v-on:handle-click="hadleClick"
      />
    </div>
  </main>
</template>

<script>
import CallQueue from "./CallQueue.vue";
import FloorsItem from "./FloorsItem.vue";

export default {
  props: ["floors", "queue", "position", "direction"],
  components: { CallQueue, FloorsItem },
  methods: {
    hadleClick(id) {
      this.$emit("handleClick", id);
    },
  },
};
</script>

<style scoped>
.main {
  width: 100%;
  padding: 10px;
  /* margin: 0 auto; */
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
  border: 3px solid rgb(130, 144, 153);
  background-color: #fff;
  border-radius: 10px;
}
</style>
