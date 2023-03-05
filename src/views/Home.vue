<template>
  <div class="home">
    <DictionaryList msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
// @ is an alias to /src
import DictionaryList from "@/components/DictionaryList.vue";

export default {
  name: "Home",
  components: {
    DictionaryList
  }
};
</script>
