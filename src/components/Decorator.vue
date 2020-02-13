<template>
  <div class="decorator-content">
    <img :src="content.url" />
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    content: Object
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.decorator-content {
  height: 100%;
}
.decorator-content img {
  width: 100%;
  height: 100%;
}
</style>
