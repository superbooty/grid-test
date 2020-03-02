<template>
  <div class="component-wrapper">
    <component :is="content.component" :content="content"></component>
  </div>
</template>

<script>
const getTwoCol = () => import( '../components/CommerceTwoCol.vue');
const getFillRow = () => import( '../components/CommerceFillRow.vue');
const getGriddy = () => import( '../components/Griddy.vue');

export default {
  name: "Decorator",
  props: {
    content: Object
  },
  components: {
    CommerceTwoCol: getTwoCol,
    CommerceFillRow: getFillRow,
    Griddy: getGriddy,
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
