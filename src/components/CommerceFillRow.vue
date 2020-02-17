<template>
  <div class="decorator-content">
    <div class="decorator-mask">
    </div>
    <img :src="content.url" />
    <div class="headline-mobile-align"><h3 data-v-43ca4d66="" class="headline-text">{{content.msg}}</h3></div>
    <div class="cta-buttons">
        <button>SHOW ME</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "CommerceTwoCol",
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
  object-fit: cover;
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
  z-index: 1001;
  color: white;
  height: 0px;
}

.headline-mobile-align h3 {
    margin: 0 !important;
    font-weight: 700;
    font-size: 20px;
    letter-spacing: .13em;
}

.cta-buttons {
  position: absolute;
  bottom: 20vh;
  display: inline;
  z-index: 1001;
  transform: translateX(-50%);
}

.cta-buttons button {
  border: 1px solid black;
  background-color: white;
  font-size: 14px;
  letter-spacing: 0.15em;
  min-width: 100px;
  max-width: 200px;
  padding: 10px 15px;
}

.cta-buttons button:hover {
  border: 1px solid white;
  background-color: black;
  color: white;
}

</style>
