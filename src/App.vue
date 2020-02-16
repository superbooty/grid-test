<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <div class="page">
      <div v-if="decorators != null" class="container-col">
        <template v-for="(d, i) in decorators">
          <div
            v-if="d.context == 'content'"
            :class="[d.pos]"
            :style="{'grid-row': d.row}"
            :key="`${d.row}-d-${i}`"
          >
            <decorator :content="d.content"></decorator>
          </div>
        </template>
        <template v-for="commerce in computedCommerce">
          <div class="item" :class="{decorated: commerce.isDecorated}" :key="commerce.product.code">
            <img :class="{'img-decorated': commerce.isDecorated}" :src="commerce.product.images[3].url" />
            <div>{{commerce.product.name}}</div>
            <div>{{commerce.product.price.formattedValue}}</div>
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
  
  data: () => ({
    decorators: [],
    cols: 3, // this value should come from testing the device type
    products: null,
  }),
  components: {
    HelloWorld,
    Decorator
  },
  methods: {
    isDecoratedCommerce(i) {
      let rowNum = (i + this.cols) / this.cols;
      rowNum = rowNum | 0;
      let itemPlacement = (i + 1 + this.cols) - (this.cols * rowNum);
      // check if item tile is decorated
      if (this.decorators != null) {
        const decorators = this.decorators.filter(decorator => {
          return decorator.row == rowNum && decorator.context === "commerce";
        });
        return decorators.length > 0 && (itemPlacement == 1 || itemPlacement == 2);
      }
      return false;
    }
  },
  computed: {
    currentDecorator() {
      return this.decorator;
    },
    computedCommerce() {
      let commerceProducts = [];
      if (this.products != null) {
        this.products.forEach((product, i) => {
          let commerceProduct = {
            product: product,
          }
          commerceProduct.isDecorated = this.isDecoratedCommerce(i);
          commerceProducts.push(commerceProduct);
        });
      }
      return commerceProducts;
    }
  },
  created() {
    fetch("mocks/decorators.json")
      .then(response => {
        return response.json();
      })
      .then(myJson => {
        console.log(myJson);
        this.decorators = myJson;
      });
    fetch("mocks/products.json")
      .then(response => {
        return response.json();
      })
      .then(myJson => {
        console.log(myJson);
        this.products = myJson;
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
  grid-auto-flow: dense;
}

.container-col .item img {
  width: 100%;
  height: auto;
  object-fit: cover;
}

.left,
.right {
  grid-column: 1 / -1;
  height: auto;
}

.side-by-side {
  grid-column: 1 / -1;
}

.fill {
  grid-column: 1 / -1;
  /* height: 250px; */
  /* border: solid black 1px; */
  /* background-color: rgb(218, 218, 218); */
  grid-auto-rows: auto;
}

.img-decorated {
  max-height: 200px;
}

.decorated {
    max-width: 75vw !important;
    grid-column: span 2 !important;
}

@media screen and (min-width: 600px) {
  .container-col {
    grid-auto-rows: auto;
    grid-auto-flow: row;
    grid-template-columns: repeat(6, 1fr);
    grid-column-gap: 15px;
    grid-row-gap: 15px;
    display: grid;
  }

  .container-col .item {
    /* border: solid black 1px; */
    grid-column: span 2;
  }

  .left {
    grid-column: 1 / 5;
  }

  .right {
    grid-column-start: 7;
    grid-column-end: 3;
  }

  .decorated {
    max-width: 25vw !important;
    grid-column: span 3 !important;
  }
}

.page {
  max-width: 800px;
  display: inline-block;
  /* width: 800px; */
}
</style>
