<template>
  <div class="component-wrapper">
    <component :is="content.component" :content="content"></component>
  </div>
</template>

<script>
import CommerceContentA from '../components/CommerceContentA.vue'

export default {
  name: "HelloWorld",
  props: {
    content: Object
  },
  components: {
    CommerceContentA,
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.component-wrapper {
  height: 100%;
  position: relative;
}
</style>
