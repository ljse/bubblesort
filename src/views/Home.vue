<template>
  <div class="home">
    <web-app />
  </div>
</template>

<script>
// @ is an alias to /src
import WebApp from "@/components/WebApp.vue";

export default {
  name: "Home",
  components: {
    WebApp,
  },
};
</script>
