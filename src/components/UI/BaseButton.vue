<template>
  <button :class="mode">
    <slot></slot>
  </button>
</template>
<script>
export default {
  props: [ 'mode'],
};
</script>
<style scoped>
button {
  padding: 0.75rem 1.5rem;
  font-family: inherit;
  background-color:darkcyan;
  border: 1px solid darkcyan;
  color: white;
  cursor: pointer;
}

button:hover,
button:active {
  background-color: rgb(2, 85, 85);
  border-color: rgb(2, 85, 85);
}

.flat {
  background-color: transparent;
  color: darkcyan;
  border: none;
}

.flat:hover,
.flat:active {
  background-color: darkcyan;
}
</style>
