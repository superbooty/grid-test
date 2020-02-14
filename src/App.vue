<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <div class="page">
      <div class="container-col">
        <template v-for="product in products">
          <div class="item" :key="product.code">
            <img :src="product.images[3].url" />
            <div>{{product.name}}</div>
            <div>{{product.price.formattedValue}}</div>
          </div>
        </template>
        <template v-for="d in decorators">
          <div :class="[d.type, d.pos]" :style="{'grid-row': d.row}" :key="`${d.row}-d`">
            <decorator :content="d.content"></decorator>
          </div>
        </template>
      </div>
    </div>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import Decorator from "./components/Decorator.vue";

export default {
  name: "App",
  decorator: null,
  data: () => ({
    decorators: null,
    cols: 3, // this value should come from testing the device type
    products: null
  }),
  components: {
    HelloWorld,
    Decorator
  },
  methods: {
    rowHasDecorator(rowNum) {
      console.log(rowNum);
      const decorators = this.decorators.filter(val => {
        console.log("FOUND :: ", val.row == rowNum);
        return val.row == rowNum;
      });
      console.log("DECORATORS :: ", decorators);
      if (decorators.length > 0) {
        this.decorator = decorators[0];
      }
      return decorators.length > 0;
    }
  },
  computed: {
    currentDecorator() {
      return this.decorator;
    }
  },
  mounted() {
    fetch("mocks/products.json")
      .then(response => {
        return response.json();
      })
      .then(myJson => {
        console.log(myJson);
        this.products = myJson;
      });

      fetch("mocks/decorators.json")
      .then(response => {
        return response.json();
      })
      .then(myJson => {
        console.log(myJson);
        this.decorators = myJson;
      });
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antiadivased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.container-col {
  justify-items: center;
  grid-auto-rows: auto;
  grid-template-columns: repeat(2, 1fr);
  grid-column-gap: 15px;
  grid-row-gap: 15px;
  display: grid;
}
.container-col .item {
  /* border: solid black 1px; */
  max-width: 250px;
}

.container-col .item img {
  width: 100%;
  /* height: auto; */
}

.two-col {
  grid-column: span 2;
  /* border: solid black 1px; */
  /* background-color: rgb(163, 194, 240); */
}

.left {
  grid-column-start: 1;
  grid-column-end: 3;
}

.right {
  grid-column-end: 3;
}

.left,
.right {
  height: auto;
}

.full {
  grid-column: 1 / -1;
  /* height: 250px; */
  /* border: solid black 1px; */
  /* background-color: rgb(218, 218, 218); */
  grid-auto-rows: auto;
}


@media screen and (min-width: 600px) {
  .container-col {
    grid-auto-rows: auto;
    grid-template-columns: repeat(3, 1fr);
    grid-column-gap: 15px;
    grid-row-gap: 15px;
    display: grid;
  }

  .left {
    grid-column-start: 1;
    grid-column-end: 3;
  }

  .right {
    grid-column-end: 4;
  }
}

.page {
  max-width: 800px;
  display: inline-block;
  /* width: 800px; */
}
</style>
