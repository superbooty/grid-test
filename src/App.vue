<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <div class="page">
      <div class="container-3-col">
        <template v-for="product in products">
          <div class="item" :key="product.code">
            <img :src="product.images[3].url" />
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
import HelloWorld from './components/HelloWorld.vue';
import Decorator from './components/Decorator.vue'

export default {
  name: 'App',
  decorator: null,
  data: () => ({
        decorators: [
          {
            row: 2,
            pos: 'none',
            type: 'full',
            content: {
              url: 'https://images.contentstack.io/v3/assets/blt2d702d64bab5cd4d/blt0630067229f3e757/5e2ff91d507d2f74fb78c3e8/20H1_EU_February_HP_Refresh_Hero_BalloonJeans_Desktop_V2.jpg?width=1560&format=pjpg&quality=90'
            }
          },
          {
            row: 3,
            pos: 'left',
            type: 'two-col',
            content: {
              url: 'https://images.contentstack.io/v3/assets/blt2d702d64bab5cd4d/blt04212de7f2aedc90/5e3030fbe147ae4537d92d1f/sh_50193_chino.jpg?width=1030&format=pjpg&quality=90'
            }
          },
          {
            row: 5,
            pos: 'right',
            type: 'two-col',
            content: {
              url: 'https://images.contentstack.io/v3/assets/blt2d702d64bab5cd4d/blt2b2050905f6ee60e/5e2edce438beb045b8566bf3/20_H1_LVC_HomepageA2_Desktop.jpg?width=538&format=pjpg&quality=90'
            }
          }
        ],
        cols: 3, // this value should come from testing the device type
        products: null,
    }),
  components: {
    HelloWorld,
    Decorator,
  },
  methods: {
      rowHasDecorator(rowNum) {
          console.log(rowNum);
          const decorators = this.decorators.filter((val) => {
            console.log('FOUND :: ', val.row == rowNum);
            return val.row == rowNum;
          });
          console.log('DECORATORS :: ', decorators);
          if (decorators.length > 0) {
            this.decorator = decorators[0];
          }
          return decorators.length > 0;
      },
  },
  computed: {
    currentDecorator() {
      return this.decorator;
    }
  },
  mounted() {
    fetch('mocks/products.json')
    .then((response) => {
      return response.json();
    })
    .then((myJson) => {
      console.log(myJson);
      this.products = myJson;
      console.log('PRODUCTS :: ', this.products);
    });
  }
}
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

.container-3-col {
  grid-auto-rows: auto;
  grid-template-columns: repeat(3, 1fr);
  grid-column-gap: 15px;
  grid-row-gap: 15px;
  display: grid;
}

.container-3-col .item {
  border: solid black 1px;
}

.container-3-col .item img {
  width: 100%;
}

.two-col {
  grid-column: span 2;
  border: solid black 1px;
  background-color: rgb(163, 194, 240);
}

.left {
  grid-column-start: 1;
  grid-column-end: 3;
}

.right {
  grid-column-end: 4;
}

.full {
  grid-column: 1 / -1;
  height: 250px;
  border: solid black 1px;
  background-color: rgb(218, 218, 218);
}

.page {
  max-width: 800px;
  display: inline-block;
  width: 800px;
}

</style>
