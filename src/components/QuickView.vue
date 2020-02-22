<template>
  <div class="qv-wrapper">
      <button class="quick-view">Quick View</button>
  </div>
</template>

<script>
export default {
  name: "QuickView",
  props: {
    content: Object
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.qv-wrapper {
  
}

.show {
    display: flex;
}

.quick-view {
  display: flex;
  justify-content: center;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translateX(-50%);
  width: 100px;
  height: 30px;
}

</style>