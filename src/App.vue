<template>
  <div class="my-5"  >
    <formulario></formulario>
  </div>
</template>

<script>
import formulario from "./components/form.vue";

export default {
  name: "App",
  components: {
    formulario,
  },
  
};
</script>

<style>
body {
    background: #F3F3F3;
}
</style>
