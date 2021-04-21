<template>
  <div>
    <p v-if="isLoading">Loading...</p>
    <h2>Shopping Chart</h2>
    <div class="cart">
      <div class="item" v-for="(item, index) in cart" :key="index">
        <div class="image">
          <a v-bind:href="item.url">
            <img v-bind:src="item.image" />
          </a>
        </div>
        <div class="info">
          <h4>{{ item.name }}</h4>
          <p class="seller">by {{ item.seller }}</p>
          <p class="status available" v-if="item.isAvailable">In Stok</p>
          <p class="shipping" v-if="item.isEligible">
            Eligible for FREE Shipping & FREE Returns
          </p>
          <a href="" v-on:click="removeFromCart(index)">Delete</a>
          <a href="" class="secondary">Save for later</a>
        </div>
      </div>
    </div>

    <h2>Saved for later {{saved.length}} item(s)</h2>
    <div class="cart">
      <div class="item" v-for="item in saved" :key="item.id">
        <div class="image">
          <a v-bind:href="item.url">
            <img v-bind:src="item.image" />
          </a>
        </div>
        <div class="info">
          <h4>{{ item.name }}</h4>
          <p class="seller">by {{ item.seller }}</p>
          <p class="status available" v-if="item.isAvailable">In Stok</p>
          <p class="shipping" v-if="item.isEligible">
            Eligible for FREE Shipping & FREE Returns
          </p>
          <a href="">Delete</a>
          <a href="" class="secondary">Move to cart</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isLoading: true,
      cart: [],
      saved: [],
    };
  },
  created() {
    setTimeout(() => {
      fetch("/static/data.json")
        .then((res) => res.json())
        .then((res) => {
          this.cart = res.cart;
          this.saved = res.saved;
          this.isLoading = false;
          return res;
        })
        .then((res) => console.log(res));
    }, 1000);
  },
  methods: {
    removeFromCart(index) {
      console.log(index);
    },
  },
};
</script>




<style>
body {
  font-size: 13px;
  line-height: 19px;
  color: #111;
  font-family: Arial, sans-serif;
  background: #fff;
}

h4,
p {
  padding: 0;
  margin: 0;
}

.item {
  border-bottom: 1px solid #ddd;
  padding: 15px 0;
  overflow: hidden;
}

.item:first-child {
  border-top: 1px solid #ddd;
}

.item img {
  width: 100px;
  height: 100px;
}

h4 {
  color: #0066c0;
  font-size: 16px;
  line-height: 1.255;
}

.image,
.info {
  float: left;
}

.image {
  margin-right: 20px;
}

.seller {
  font-size: 13px;
  line-height: 19px;
}

.status.available {
  color: #008a00;
  font-size: 12px;
  line-height: 1.5;
}

.shipping {
  color: #555;
  font-size: 12px;
  line-height: 1.5;
}

.info a {
  color: #0066c0;
  font-size: 12px;
  text-decoration: none;
  line-height: 24px;
}

.saved-header {
  margin-top: 50px;
}

a.secondary {
  padding-left: 5px;
  margin-left: 3px;
  border-left: 1px solid #ccc;
}
</style>