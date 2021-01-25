<template>
  <div>
    <dialog open>
      <slot></slot>
    </dialog>
  </div>
</template>

<script>
export default {
  
}
</script>

<style scoped>
div {
  position: fixed;
  background-color: rgba(0,0,0,0.1);
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}
dialog {
  margin: 0;
  position: fixed;
  top: 20vh;
  left: 30%;
  width: 40%;
  background-color: white;
  box-shadow: 0 2px 8px rgba(0,0,0,0.26);
  padding: 1rem;
}
</style>