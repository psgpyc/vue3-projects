<template>
  <div class="card-wrapper">
    <slot></slot>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.card-wrapper {
  height: 450px;
  width: 60%;
  margin: 10px auto;
  box-shadow: 0 1px 6px rgb(32 33 36 / 28%);
  border-color: rgba(223, 225, 229, 0);
  border-radius: 5px;
  overflow: scroll;
}
</style>
