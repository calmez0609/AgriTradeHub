<template>
  <div class="home">
    <NavBar /> <!-- 引入 NavBar 組件 -->
    <HeaderView/> <!-- 引入 Header 組件 -->
    <div class="content">
            <CropSearchBar />
    </div>
  </div>
</template>

<script>
// Import the necessary components
import NavBar from "@/components/NavBar.vue";
import HeaderView from "@/components/HeaderView.vue"; // Import Header component
import CropSearchBar from "@/components/CropSearchBar.vue"; // Import CropSearchBar component

export default {
  name: "HomeView",
  components: {
    NavBar,
    HeaderView, // Register Header component
    CropSearchBar, // Register CropSearchBar component
  },
};
</script>

<style scoped>
/* You can add custom styles here for HomeView */
.home {

}

.content {
  margin-top: 20px;
}

h1 {
  color: #4CAF50;
}

p {
  font-size: 18px;
  color: #555;
}
</style>
