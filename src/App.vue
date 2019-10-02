<template>
  <div id="app">
    <section class="collectiontwo section-padding">
      <div class="container text-center position-relative">
        <div class="row my-5">
          <div class="cart-drawer" :class="openedcart ? 'opened':'remove'" @click.stop>
            <div
              class="drawer-header d-flex justify-content-between align-items-center px-4 py-4 bg-bg"
            >
              <h6 class="text-uppercase my-0">Shopping Bag</h6>
              <a
                href="#"
                rel="nofollow"
                aria-label="Close"
                title="Close"
                class="btn-close float-right">
                <i class="icon ion-md-close closeicon" @click.prevent="removeadd()"></i>
              </a>
            </div>
            <div class="row cart-item m-0">
              <cartitem
                :cartitems="items"
                :index="index"
                :qty="qty"
                :d-index="dIndex"
                v-for="(items, index) in cartListItem"
                :key="index"
                @inc="increase"
                @dec="decrease"
                @remove="removeitem"
              ></cartitem>
            </div>
            <div class="drawer-footer p-7 bg-gray-200 text-center mt-auto">
              <div id="ap-cart" class="d-flex justify-content-between align-items-center mb-2">
                <p class="price">
                  <span class="h6 d-inline-block">Subtotal</span>
                  <span class="h6">$ {{addprice()}}.00</span>
                </p>
              </div>
              <p class="font-italic mb-2 line-height-sm">
                <small>Shipping &amp; taxes are calculated during checkout.</small>
              </p>
              <div role="group" class="btn-group btn-group-sm btn-group-justified">
                <a href="/cart" class="btn btn-primary d-none">View Cart</a>
                <a class="btn btn-primary text-white">
                  Checkout
                  <i class="icon ion-md-arrow-forward"></i>
                </a>
              </div>
            </div>
          </div>
   <sellertemp @open="open" @add="add" :seller="item" v-for="(item, index) in arrItems" :key="index" :index="index"
                    @get-index="getIndex" @addcart="addtocartlist" >
                </sellertemp>
         

          <div>
            <quicktemp
              v-show="isactive"
              :cartitems="cartListItem"
              @close="close"
              :arr-items="arrItems"
              class="bg-white"
              :d-index="dIndex"
              @addcart="addtocartlist"
              @add="add"
              @inc="increase"
              @dec="decrease"
              @remove-popup="close"
            
            ></quicktemp>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import sellertemp from "../src/components/seller";
import quicktemp from "../src/components/quickview";
import cartitem from "../src/components/cartdrawer";


export default {
  name: "app",
  components: {
    sellertemp,
    quicktemp,
    cartitem,
   
  },
  data() {
    return {
      arrItems: [],
      file: "https://curlmix.com/collections/all?view=products.json",
      dIndex: -1,
      isactive: false,
      openedcart: false,
      cartListItem: [],
      qty: [],
      price: 0
    };
  },
  mounted() {
    this.init();
  },
  methods: {
    init: function() {
      this.render();
    },
    addtocartlist() {
      let temp = this.arrItems[this.dIndex].id;

      let flag = 0;
      const s = this.cartListItem;

      if (s.length != 0) {
        for (let i = 0; i < s.length; i++) {
          if (temp === s[i].id) {
            this.arrItems[this.dIndex].compare_at_price_min++;

            flag = 1;
            break;
          }
        }
        if (flag === 0) {
          s.push(this.arrItems[this.dIndex]); //else push the item
        }
      } else {
        s.push(this.arrItems[this.dIndex]);
      }
    },
    increase() {
      this.arrItems[this.dIndex].compare_at_price_min++;
    },
    decrease() {
      if (this.arrItems[this.dIndex].compare_at_price_min > 0) {
        this.arrItems[this.dIndex].compare_at_price_min--;
      }
    },
    getIndex(index) {
      this.dIndex = index;
    },
    open() {
      this.isactive = true;
    },
    close() {
      this.isactive = false;
    },
    Close() {
      if (this.isactive === true) {
        this.close();
      } else if (this.openedcart === true) {
        this.removeadd();
      }
    },
    add() {
      this.openedcart = true;
    },
    removeadd() {
      this.openedcart = false;
    },
    removeitem(index) {
      this.cartListItem.splice(index, 1);
    },
    addprice() {
      let sum = 0;
      for (let p = 0; p < this.cartListItem.length; p++) {
        sum +=
          ((this.cartListItem[p].compare_at_price_min + 1) *
            this.cartListItem[p].price) /
          100;
      }
      return sum;
    },
    render: async function() {
      try {
        const response = await fetch(this.file);
        var data = await response.json();
      } catch (error) {
        alert(error);
      }
      data.forEach(data => {
        this.arrItems.push(data);
        this.qty.push(1);
      });
    }
  }
};
</script>
<style lang="css">
@import "../node_modules/bootstrap/scss/bootstrap.css";
@import "../node_modules/ionicons/dist/css/ionicons.css";
</style>