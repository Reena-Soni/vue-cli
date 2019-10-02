<template>
  <div class="row w-100 m-0">
    <div class="col-lg-3">
      <img :src="cartitems.images[0]" class="card-img" alt="..." />
    </div>
    <div class="col-lg-6 mt-2 col-mx-8">
      <div class="card-body">
        <p class="card-title mb-6 mb-lg-0">{{cartitems.title}}</p>
        <div class="quantity-wrapper d-inline-flex mt-mx-5 mt-lg-0">
          <div class="input-group input-group-sm">
            <div class="input-group-prepend">
              <a
                href="#"
                title="Decrease"
                class="input-group-text bg-transparent border-right-0 border-secondary"
                @click="$emit('dec')"
              >
                <span class="btn-decrease"></span>
              </a>
            </div>
            <input
              type="text"
              name="quantity"
              aria-label="quantity"
              :value="cartitems.compare_at_price_min+1"
              step="1"
              min="1"
              class="quantity py-4 px-3 form-control border-secondary font-weight-bolder text-center border-left-0 border-right-0 bg-transparent"
            />
            <div class="input-group-append">
              <a
                href="#"
                title="Increase"
                class="input-group-text bg-transparent border-left-0 border-secondary"
                @click="$emit('inc')"
              >
                <span class="btn-increase"></span>
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="col-lg-3">
      <a href="#" class="cartremove" @click="removeItem">
        <img src="assets/images/remove.png" alt />
      </a>
      <h6>$ {{((cartitems.price)/100)*(cartitems.compare_at_price_min+1)}}</h6>
    </div>
  </div>
</template>


<script>
export default {
  name: "cartitem",
  props: {
    cartitems: {
      type: Object,
      required: true
    },
    dIndex: {
      type: Number,
      required: true
    },
    index: {
      type: Number,
      required: true
    },
    qty: {
      type: Array,
      required: true
    }
  },
  methods: {
    removeItem() {
      this.$emit("remove", this.index);
    }
  }
};
</script>