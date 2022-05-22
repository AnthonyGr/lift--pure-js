<template>
  <div class="queue">{{ queue }}</div>
</template>

<script>
export default {
  props: ["queue"],
};
</script>

<style scoped>
.queue {
  width: 200px;
  padding: 5px 10px;
  height: 20px;
  border: 3px solid rgb(130, 144, 153);
  border-radius: 10px;
  word-wrap: break-word;
}
</style>
