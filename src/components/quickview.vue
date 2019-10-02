<template>
  <div class="row position-fixed" id="prod" @click.stop>
    <div class="col-lg-6">
      <div class="row mt-4">
        <div class="col-lg-10 col-md-10 order-md-2 mt-md-0 mt-3">
          <flickity class="carousel-main" ref="flickity" :options="flickityOptions" >
            <img :src="arrItems[this.dIndex].images[0]" alt class="w-100" />
            <img :src="arrItems[this.dIndex].images[1]" alt class="w-100" />
            <img :src="arrItems[this.dIndex].images[2]" alt class="w-100" />
            <img :src="arrItems[this.dIndex].images[3]" alt class="w-100" />
            <img :src="arrItems[this.dIndex].images[4]" alt class="w-100" />
          </flickity>
        </div>
      </div>
    </div>
    <div class="col-lg-6 my-6 text-lg-left">
      <span class="d-flex justify-content-end">
        <a href="#">
          <i class="ion ion-md-close" @click.prevent="$emit('close')"></i>
        </a>
      </span>
      <p>STEP 4 OF WASH + GO SYSTEM</p>
      <h2>{{arrItems[dIndex].title}}</h2>
      <div class="row">
        <div class="col-sm-6">
          <p class="price">
            {{arrItems[dIndex].title}}
            <span class="ml-2">
              <small class="text-muted">8 oz. bottle</small>
            </span>
          </p>
        </div>
        <div class="col-sm-6 d-sm-flex justify-content-end">
          <span>
            <img src="assets/images/star.png" alt />
          </span>
          <span class="mt-1 custom">43 Reviews</span>
        </div>
      </div>
      <form>
        <div class="quantity-wrapper d-inline-flex mt-3 mb-mx-3">
          <div class="input-group input-group-sm mt-1">
            <div class="input-group-prepend">
              <a
                href="#"
                title="Decrease"
                @click.prevent="$emit('dec')"
                class="input-group-text bg-transparent border-right-0 border-secondary"
              >
                <span class="btn-decrease"></span>
              </a>
            </div>
            <input
              type="text"
              name="quantity"
              aria-label="quantity"
              :value="arrItems[dIndex].compare_at_price_min+1"
              step="1"
              min="1"
              class="quantity py-4 px-3 form-control border-secondary font-weight-bolder text-center border-left-0 border-right-0 bg-transparent"
            />
            <div class="input-group-append">
              <a
                href="#"
                title="Increase"
                @click.prevent="$emit('inc')"
                class="input-group-text bg-transparent border-left-0 border-secondary"
              >
                <span class="btn-increase"></span>
              </a>
            </div>
          </div>
        </div>
        <a
          href="#"
          class="btn btn-primary addToCart text-uppercase text-white px-8 px-sm-5 py-2 mb-1 ml-lg-3 font-weight-bold"
          @click.stop
          @click.prevent="cartList(index);$emit('add');$emit('addcart');$emit('remove-popup')"
        >add to bag</a>
      </form>
    </div>
  </div>
</template>
<script>
import Flickity from 'vue-flickity'
export default {
  name: 'quicktemp',
  components: {
    Flickity
  },
  props: {
    dIndex: {
      type: Number
    },
    arrItems: {
      type: Array
    }
  },
  data(){
    return{
      flickityOptions: {
        draggable: true,
        groupCells: false,
        pageDots: false,
        prevNextButtons: false,
        arrowShape: { x0: 10, x1: 60, y1: 50, x2: 70, y2: 45, x3: 25 },
        wrapAround: true
        
        // any options from Flickity can be used
      },
    }
  },
  methods: {
    cartList: function(index) {
      this.$emit("get-index", index);
    }
  }
};
</script>
