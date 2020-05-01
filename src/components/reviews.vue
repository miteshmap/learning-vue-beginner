<template>
  <div class="product-reviews">
    <form @submit.prevent="saveReviews">
      <div>
        <label>Name:</label>
        <input type="text" name="name" v-model="name">
      </div>
      <div>
        <label>Review:</label>
        <textarea name="review" v-model="review"></textarea>
      </div>
      <div>
        <label>Rating:</label>
        <select name="rating" v-model.number="rating">
          <option v-for="index in range(1, 5)" :key="index">{{ index }}</option>
        </select>
      </div>
      <button type="submit">Save</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "reviews",
  data() {
    return {
      name: "",
      review: "",
      rating: ""
    };
  },
  methods: {
    range(start, end) {
      var ranges = [];
      for (let i = start; i <= end; i++) {
        ranges.push(i);
      }
      return ranges;
    },
    saveReviews() {
      console.log({
        name: this.name,
        review: this.review,
        rating: this.rating
      });
    }
  }
};
</script>
