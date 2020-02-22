<template>
  <div id="app">
    <Header msg="Content and Commerce Category Page" />
    <svg class="logo" viewBox="0 0 77 32" id="levi-logo"><path d="M61.403 19.729c-4.692 0-5.547-2.747-5.547-3.428h3.398c0 .4.535.879.986 1.074a2.882 2.882 0 001.177.192h-.006c.957 0 1.742-.235 1.742-.798 0-.686-.804-.838-1.69-.966-2.413-.353-5.794-.763-5.794-3.498 0-2.551 2.749-3.849 5.667-3.849 4.672 0 5.91 2.623 5.91 3.382h-3.453a1.147 1.147 0 00-.634-.908l-.007-.003a3.024 3.024 0 00-1.357-.335h-.002c-1.29 0-2.016.272-2.016.871 0 .489.654.732 1.594.895 2.453.427 6.219.575 6.219 3.599 0 1.536-1.313 3.77-6.186 3.77zm-5.764-9.675l-1.323 1.458h-.55l.606-1.59H53.16v-2.12h2.479zm-7.69-1.343h4.391v10.713h-4.391zm-5.726 10.734h-3.837L32.657 8.731h5.17l3.288 6.512.09.196.082-.196 3.074-6.512h3.104zm-8.243-4.451h-8.886a2.529 2.529 0 002.719 2.44l-.009.001a2.714 2.714 0 002.347-1.136l.006-.008H33.7c-1.158 2.697-3.405 3.463-6.467 3.463-3.983 0-6.799-2.185-6.799-5.647 0-3.697 2.774-5.648 6.799-5.648 4.503 0 6.761 2.957 6.761 5.803a5.486 5.486 0 01-.017.753l.002-.021zm-13.621 4.434H10.232V8.74h4.553v7.78h5.574zM72.236 0c.032.067.068.132.098.201.268.607.424 1.316.424 2.061v.045-.002.054c0 .754-.156 1.471-.437 2.121l.013-.035a5.473 5.473 0 01-1.144 1.701 5.135 5.135 0 01-1.646 1.11l-.034.013a5.188 5.188 0 01-2.015.401h-.035.002-.029c-.73 0-1.426-.147-2.059-.414l.035.013a5.243 5.243 0 01-1.695-1.123 5.403 5.403 0 01-1.136-1.666l-.013-.035a5.253 5.253 0 01-.425-2.086v-.057V2.262c0-.745.156-1.453.438-2.094l-.013.033c.03-.069.066-.134.099-.201H.001L7.41 32c15.555-10.136 30.504-.395 31.106-.024h.002l.004-.003h.008l.004.002.003.001c.6-.372 15.551-10.112 31.105.024L77.05 0zM27.148 10.699h-.017a2.048 2.048 0 00-2.048 2.048l.002.1v-.005h4.301a2.027 2.027 0 00-2.249-2.143l.009-.001zM64.35 5.581a4.237 4.237 0 003.072 1.316h.042-.002.037c.605 0 1.18-.129 1.699-.361l-.026.011a4.306 4.306 0 001.376-.964l.002-.002c.385-.407.695-.889.907-1.421l.011-.03c.21-.527.332-1.139.332-1.778v-.049V2.269a4.77 4.77 0 00-.344-1.784l.011.032a4.705 4.705 0 00-.26-.54l.012.023h-1.502c.147.266.233.584.233.922l-.001.07V.989a1.522 1.522 0 01-.466 1.236l-.001.001c-.315.26-.714.43-1.15.465h-.007l1.765 2.761h-1.031L67.38 2.763h-1.017v2.689h-.959V0h-1.723c-.08.14-.163.31-.236.485l-.012.031a4.697 4.697 0 00-.332 1.75v.039-.002.048c0 .639.122 1.25.344 1.81l-.012-.033c.222.563.532 1.045.919 1.454l-.002-.002zm3.629-3.627c.189-.011.364-.054.525-.125l-.01.004a.813.813 0 00.358-.304l.002-.003c.086-.15.136-.329.136-.52l-.002-.062v.003l.001-.043a.933.933 0 00-.123-.463l.002.005a.828.828 0 00-.307-.284L68.557.16a1.302 1.302 0 00-.431-.134l-.007-.001a3.097 3.097 0 00-.211-.024h-1.546v1.975h1.002q.325 0 .614-.021z"></path></svg>
    <div class="separator"></div>
    <div class="page">
      <div v-if="decorators != null" class="container-col">
        <template v-for="(commerce, i) in computedCommerce">
          <div class="item" :class="{decorated: commerce.decoratedRow && commerce.itemPlacement < 3 }"
            :style="[commerce.decoratedRow && commerce.itemPlacement < 3  ? {'grid-row' : commerce.row} : '']"
            :key="commerce.product.code" @mouseenter="toggleQickViewBtn(i)" @mouseleave="toggleQickViewBtn(i)">
            <img :class="{'img-decorated': commerce.isDecorated}" :src="commerce.product.images[3].url" />
            <quick-view v-show="qvButtons[selected]" :class="{'one' : qvButtons}"/>
            <div>{{commerce.product.name}}</div>
            <div class="color">Color: {{commerce.product.colorName}}</div>
            <div>{{commerce.product.price.formattedValue}}</div>
          </div>
        </template>
        <template v-for="(d, i) in decorators.content">
          <div
            :class="[d.pos]"
            :style="{'grid-row': d.row}"
            :key="`${d.row}-d-${i}`"
          >
            <decorator :content="d.content"></decorator>
          </div>
        </template>
      </div>
    </div>
  </div>
</template>

<script>
import Decorator from "./components/Decorator.vue";
import Header from "./components/Header.vue";
import QuickView from "./components/QuickView.vue";

export default {
  name: "App",
  
  data: () => ({
    decorators: [],
    cols: 2, // this value should come from testing the device type
    products: null,
    qvButtonsState: [],
    selected: 0,
  }),
  components: {
    Header,
    Decorator,
    QuickView
  },
  methods: {
    isDecoratedCommerce(i) {
      let rowNum = (i + this.cols) / this.cols;
      rowNum = rowNum | 0;
      // let itemPlacement = (i + 1 + this.cols) - (this.cols * rowNum);
      console.log("ROW :: ", rowNum);
      // check if item tile is decorated
      // let caonDecorateCommerce = false;
      // if (this.cols > 2 && (itemPlacement == 1 || itemPlacement == 2)) {
      //   caonDecorateCommerce = true;
      // }
      // if (this.cols < 3 && itemPlacement == 1) {
      //   caonDecorateCommerce = true;
      // }
      // if (this.decorators != null) {
      //   const decorators = this.decorators.commerce.filter(decorator => {
      //     return decorator.row == rowNum ;
      //   });
      //   return decorators.length > 0 && caonDecorateCommerce;
      // }
      return false;
    },
    getCommerceDecorator(i) {
      let rowNum = (i + this.cols) / this.cols;
      rowNum = rowNum | 0;
      let decorators = null;
      if (this.decorators != null) {
        decorators = this.decorators.commerce.filter(decorator => {
          return decorator.row == rowNum ;
        });
      }
      return decorators.length > 0 ? decorators[0] : null;
    },
    toggleQickViewBtn(i) {
      console.log("MOUSER");
      this.selected = i;
      this.qvButtonsState[i] = !this.qvButtonsState[i];
      // this.quickViewBtnActive = !this.quickViewBtnActive;
    },
    isRowDecorated(row) {
      let decorators = null;
      if (this.decorators != null) {
        decorators = this.decorators.content.filter(decorator => {
          return decorator.row == row ;
        });
      }
      return decorators.length > 0 ? decorators[0] : false;
    },
    isInDecoratedRow(commerce) {
      let decorators = null;
      if (this.decorators != null) {
        decorators = this.decorators.commerce.filter(decorator => {
          return decorator.row == commerce.row ;
        });
      }
      return decorators.length > 0; 
    },
    canDecorate(i) {
        return (i + 1 + 2 ) % this.cols != 0;
    }
  },
  computed: {
    currentDecorator() {
      return this.decorator;
    },
    qvButtons() {      
      return this.qvButtonsState;
    },
    computedCommerce() {
      let commerceProducts = [];
      let colsCount = 0;
      if (this.products != null) {
        this.products.forEach((product, i) => {
          let commerceProduct = {
            product: product,
          }
          commerceProduct.isDecorated = false;
          // let decorator = null;
          // if (this.isDecoratedCommerce(i)) {
          //   commerceProduct.isDecorated = this.isDecoratedCommerce(i);
          //   decorator = this.getCommerceDecorator(i)
          // }
          let rowNum = (i + this.cols + colsCount) / this.cols;
          rowNum = rowNum | 0;
          console.log("ROW :: ", rowNum);
          let contentDecorator = this.isRowDecorated(rowNum)
          if (contentDecorator) {
            colsCount += contentDecorator.cols
          }
          commerceProduct.row = rowNum;
          commerceProduct.position = (i + 1 + colsCount);
          let itemPlacement = (commerceProduct.position + this.cols) - (this.cols * rowNum);
          console.log('PLACE :: ', itemPlacement);
          commerceProduct.itemPlacement = itemPlacement;
          if (commerceProduct.row === 2) {
            commerceProduct.decoratedRow = 2;
          }
          console.log('PRODUCT :: ', commerceProduct);
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
        this.products.forEach((product, i) => {
          this.qvButtonsState[i] = false;
        });
      });
  },
  mounted() {
    const width = window.innerWidth;
    if (width < 600) {
      this.cols = 2;
    } else {
      this.cols = 3;
    }
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

.container-col .item {
  font-family: Arial, Helvetica, sans-serif;
  font-size: 13px;
  font-weight: 400;
  text-align: left;
  line-height: 16px;
  position: relative;
}

.item .color {
  color: darkgrey;
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
    max-width: 100% !important;
    width: 75%;
    grid-column: 1 / 3 !important;
    transition: width 250ms;
}

.logo {
    height: 24px;
    width: 58px;
}
.separator {
  height: 40px;
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

  .container-col .item:hover {
    border: solid #cacaca 1px;
    padding: 3px;
  }

  .left {
    grid-column: 1 / 5;
  }

  .right {
    grid-column-start: 7;
    grid-column-end: 3;
  }

  .decorated {
    width: 60%;
    grid-column: span 3 !important;
  }

  .decorated:hover {
    width: 100%;
  }

}

.page {
  max-width: 800px;
  display: inline-block;
  /* width: 800px; */
}
</style>
