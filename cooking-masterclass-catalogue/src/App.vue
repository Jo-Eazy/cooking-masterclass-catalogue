<script setup>
import { ref } from 'vue';
import TheHeader from './components/TheHeader.vue';
import CourseCard from './components/CourseCard.vue';

const courses = ref([
  { id: 1, title: 'Italian Pasta Perfection', chef: 'Chef Luigi', price: 59.99, level: 'Intermediate', available: true },
  { id: 2, title: 'Sushi Rolling Basics', chef: 'Chef Sato', price: 49.99, level: 'Beginner', available: true },
  { id: 3, title: 'French Pastry Masterclass', chef: 'Chef Gordon', price: 79.99, level: 'Advanced', available: false },
  { id: 4, title: 'Vegan Comfort Foods', chef: 'Chef Marie', price: 45.00, level: 'Beginner', available: true },
]);

const wishlistCount = ref(0);

// Function passed down to children to update the count
const updateWishlist = (isSaved) => {
  if (isSaved) {
    wishlistCount.value++;
  } else {
    wishlistCount.value--;
  }
};
</script>

<template>
  <div class="app-container">
    <TheHeader :count="wishlistCount" />

    <main class="catalogue">
      <CourseCard
        v-for="course in courses"
        :key="course.id"
        :course="course"
        @add-to-wishlist="updateWishlist"
      />
    </main>
  </div>
</template>

<style>
/*Global Styles*/
body {
  font-family: Arial, sans-serif;
  background-color: #f8f9fa;
  margin: 0;
  padding: 0;
}

.app-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

.catalogue {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 20px;
  margin-top: 20px;
}
</style>
