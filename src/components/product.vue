<template>
  <div class="product-wrapper">
    <div class="product-media">
      <img :src="image" height="200px">
    </div>
    <div class="product-info">
      <h3>{{ title }}</h3>
      <div class="stock-info">
        <label>stock:</label>
        <span :class="stockClass">{{ stockInfo }}</span>
      </div>
      <div class="product-features">
        <ul>
          <li>
            <h4>Features:</h4>
          </li>
          <li v-for="feature in features" :key="feature">{{ feature }}</li>
        </ul>
      </div>
      <div class="variants">
        <div class="variant-colors">
          <span
            v-for="(variant, variantKey ) in variants"
            :key="variantKey"
            :class="{active: (selectedVariant == variantKey)}"
            :style="{backgroundColor: variant.color}"
            @click="changeVariant(variantKey)"
          >{{ variant.title }}</span>
        </div>
      </div>
      <div class="add-to-cart-form">
        <div class="qty-box">
          <button @click="qtyChange('remove')">-</button>
          <span>{{ qty }}</span>
          <button @click="qtyChange('add')">+</button>
        </div>
        <button type="button" @click.prevent="addToCart">Add to Cart</button>
      </div>
    </div>
    <div class="reviews">
      <reviews/>
    </div>
  </div>
</template>


<script>
import reviews from "./reviews";
export default {
  name: "product",
  components: {
    reviews
  },
  data() {
    return {
      title: "Dish washing gloves",
      selectedVariant: "grey",
      qty: 1,
      features: [
        "Heat Resistent",
        "Material",
        "Multiple Usage",
        "Ideal Kitchen Gadget",
        "Perfect Protector"
      ],
      variants: {
        grey: {
          title: "Grey",
          img: require("../assets/gloves-grey.jpg"),
          price: 200,
          stock: 20,
          color: "#ccc"
        },
        green: {
          title: "Green",
          img: require("../assets/gloves-green.jpg"),
          price: 210,
          stock: 9,
          color: "#0ef0ca"
        },
        pink: {
          title: "Pink",
          img: require("../assets/gloves-pink.jpg"),
          price: 180,
          stock: 0,
          color: "#ffc0cb"
        }
      }
    };
  },
  computed: {
    image: function() {
      return this.variants[this.selectedVariant].img;
    },
    stockStatus() {
      return this.variants[this.selectedVariant].stock;
    },
    stockInfo() {
      if (this.stockStatus > 10) {
        return "In stock";
      }
      if (this.stockStatus < 10 && this.stockStatus > 0) {
        return "Selling fast!";
      }
      if (this.stockStatus === 0) {
        return "out of stock";
      }
    },
    stockClass() {
      if (this.stockStatus > 10) {
        return "active";
      }
      if (this.stockStatus < 10 && this.stockStatus > 0) {
        return "low";
      }
      if (this.stockStatus === 0) {
        return "out-of-stock";
      }
    }
  },
  methods: {
    addToCart() {
      console.log(this.selectedVariant);
    },
    qtyChange(action) {
      if (action === "add") {
        if (this.qty < this.stockStatus) {
          this.qty++;
        }
      }
      if (action === "remove") {
        if (this.qty > 0) {
          this.qty--;
        }
      }
    },
    changeVariant(key) {
      this.selectedVariant = key;
      this.qty = this.stockStatus > 0 ? 1 : 0;
    }
  }
};
</script>


<style>
.product-wrapper {
  display: block;
}
.product-media {
  display: inline-block;
  margin: 10px;
  height: 500px;
  vertical-align: top;
}
.product-info {
  display: inline-block;
  margin: 10px;
  height: 500px;
}

.product-features {
  display: block;
  text-align: left;
}

.product-features li:first-child {
  list-style: none;
}

.product-features h4 {
  display: block;
  text-align: left;
}

.variants {
  display: block;
  padding: 10px;
}

.variant-colors span {
  display: inline-block;
  color: black;
  padding: 10px;
  margin: 0 5px;
}

.variant-colors span.active {
  font-weight: bold;
}

.stock-info {
  display: block;
  text-align: left;
  padding-left: 15px;
}

.stock-info label,
.stock-info span {
  display: inline-block;
  margin: 0 5px;
}

.stock-info span {
  padding: 5px;
}

.stock-info .active {
  background-color: green;
  color: white;
}

.stock-info .low {
  background-color: orange;
  color: black;
}

.stock-info .out-of-stock {
  background-color: red;
  color: white;
}

.add-to-cart-form .qty-box,
.add-to-cart-form > button {
  display: inline-block;
  margin: 5px;
}

.qty-box {
  display: block;
  border: 1px solid black;
}

.qty-box button,
.qty-box span {
  display: inline-block;
  font-size: 18px;
}

.qty-box span {
  padding-left: 5px;
  padding-right: 5px;
  width: 25px;
}

.qty-box button {
  border: none;
  background: black;
  color: white;
  font-weight: bold;
  text-align: center;
  padding: 5px 10px;
}
</style>
