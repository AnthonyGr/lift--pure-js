<template>
  <div class="floor">
    <div class="floor__shaft"></div>
    <div class="floor__button">
      <button
        :data-id="floor.id"
        class="btn"
        :class="{ 'non-active': floor.id === 1 }"
        :disabled="floor.isDisabled"
        v-on:click="$emit('handle-click', floor.id)"
      >
        {{ floor.title }}
      </button>
    </div>
    <LiftItem
      v-if="floor.id === 1"
      v-bind:position="position"
      v-bind:direction="direction"
    />
  </div>
</template>

<script>
import LiftItem from "./LiftItem.vue";
export default {
  components: { LiftItem },
  props: ["floor", "position", "direction"],
};
</script>

<style>
.floor {
  display: flex;
}

.floor__shaft {
  width: 100px;
  height: 100px;
  border: 1px dashed lightgray;
}

.floor__button {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-left: 10px;
}

.btn {
  width: 30px;
  height: 30px;
  padding: 5px;
  /* transition: all 0.3s; */
  cursor: pointer;
  border: 1px solid black;
  border-radius: 50%;
  color: #336699;
}

.btn:disabled {
  background-color: lightgreen;
}

.non-active {
  background-color: lightgrey !important;
}
</style>
