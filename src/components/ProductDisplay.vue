<template lang="">
  <div id="app">

    <div id="loader" class="center"></div>

    <div class="container">
      <div class="container-bg">
        <span class="background-women" v-if="nextWomen"></span>
        <span class="background-mens" v-if="nextMens" ></span>
        <span class="background-unavailable" v-if="nextAnavailable"></span>
      </div>

      <div class="card">
        <div class="product-img">
          <img class="img-detail women" v-if="nextWomen"  :src="products.image" alt="baju" >
          <img class="img-detail mens" v-if="nextMens" :src="products.image" alt="baju">
          <p class="img-unavailable" v-if="nextAnavailable"></p>
          <p class="text-unavailable" v-if="nextAnavailable">This product is unavailable to show</p>
        </div>

        <div class="product-title">
          <p class="product-title-women" v-if="nextWomen">{{products.title}}</p>
          <p class="product-title-mens" v-if="nextMens">{{ products.title}}</p>
          <p class="product-title-unavailable" v-if="nextAnavailable"></p>
        </div>

        <div class="product-category" >
          <span v-if="nextWomen">{{products.category}}</span>
          <span v-if="nextMens">{{products.category}}</span>
          <span v-if="nextAnavailable"></span>
        </div>

        <div class="product-rating">
          <span v-if="nextWomen" >{{products.rating.rate}}/5</span>
          <span v-if="nextMens" >{{products.rating.rate}}/5</span>
        </div>

        <div class="women-rating" v-if="nextWomen">
          <span class="women-rating-1" ></span>
          <span class="women-rating-2" ></span>
          <span class="women-rating-3" ></span>
          <span class="women-rating-4" ></span>
          <span class="women-rating-5" ></span>
        </div>

        <div class="mens-rating" v-if="nextMens">
          <span class="mens-rating-1" ></span>
          <span class="mens-rating-2" ></span>
          <span class="mens-rating-3" ></span>
          <span class="mens-rating-4" ></span>
          <span class="mens-rating-5" ></span>
        </div>

        <div class="product-description">
          <hr class="line-top" v-if="nextWomen">
          <hr class="line-top" v-if="nextMens">
          <p  class="product-description" v-if="nextWomen">{{products.description}}</p>
          <p  class="product-description" v-if="nextMens">{{products.description}}</p>
          <p class="product-description" v-if="nextAnavailable"></p>
          <hr class="line-buttom" v-if="nextWomen">
          <hr class="line-buttom" v-if="nextMens">
        </div>

        <div class="product-price">
          <span class="price-women" v-if="nextWomen">${{products.price}}</span>
          <span class="price-mens" v-if="nextMens">${{products.price}}</span>
        </div>

        <div class="button">
          <button class="button-women-buy" v-if="nextWomen">Buy Now</button>
          <button class="button-mens-buy" v-if="nextMens">Buy Now</button>
          <button class="button-women-next" v-if="nextWomen" v-on:click="women">Next Product</button>
          <button class="button-mens-next" v-if="nextMens" v-on:click="mens">Next Product</button>
          <button class="button-unavailable" v-if="nextAnavailable" v-on:click="unavailable">Next Product</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  data () {
    return {
      nextWomen: true,
      nextMens:false,
			nextAnavailable: false,
      products: '',
    }
  },
  
  beforeCreate() {
    let api = "https://fakestoreapi.com/products/16"
    fetch (api)
    .then((result) => result.json())
    .then((data) => (this.products = data))
},

  methods: {  

    async women(){
      const api = await fetch ('https://fakestoreapi.com/products/4');
      const response = await api.json()
      const data = response 
      console.log(this.products = data);

      this.nextAnavailable = false;
      this.nextWomen = false;
      this.nextMens = true;
    },

    async mens(){
      const api = await fetch ('https://fakestoreapi.com/products/16');
      const response = await api.json()
      const data = response 
      console.log(this.products = data);

      this.nextAnavailable = true;
      this.nextWomen = false;
      this.nextMens = false;
    },

    unavailable(){
      this.nextWomen = true;
      this.nextAnavailable = false;
      this.nextMens = false;
    }
  }
}
</script>




