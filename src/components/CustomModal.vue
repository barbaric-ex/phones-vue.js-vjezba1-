<template>
  <div class="custom-modal">
    <slot name="default"></slot>
    <slot name="stores"></slot>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.custom-modal {
  width: 600px;
  height: 500px;
  position: absolute;
  background-color: peachpuff;
  box-shadow: 0 0 8px black;
  top: 100px;
  left: 50%;
  transform: translateX(-50%);
}
</style>
