<template>
  <div class="decorator-content">
    <div class="decorator-mask">
    </div>
    <img :src="content.url" />
    <div class="headline-mobile-align"><h3 data-v-43ca4d66="" class="headline-text">{{content.msg}}</h3></div>
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
  position: relative;
}
.decorator-content img {
  width: 100%;
  height: 100%;
  display: block;
}

.decorator-mask {
  background-color: #4f4f4f;
  z-index: 1000;
  opacity: 0.2;
  height: 100%;
  width: 100%;
  position: absolute;
}

.headline-mobile-align {
  position: relative;
  top: -50%;
  color: white;
  height: 0px;
}

.headline-mobile-align h3 {
  margin: 0 !important;
}

</style>
