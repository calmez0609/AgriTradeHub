<template>
  <div class="home">
    <NavBar /> <!-- 引入 NavBar 組件 -->
    <HeaderView /> <!-- 引入 HeaderView 組件 -->
    <div class="content">
      <CropSearchBar />
    </div>
    <!-- 傳遞 API 資料給 ShowRecord 組件 -->
    <ShowRecord :records="records" />
  </div>
</template>

<script>
import axios from "axios";
import NavBar from "@/components/NavBar.vue";
import HeaderView from "@/components/HeaderView.vue";
import CropSearchBar from "@/components/CropSearchBar.vue";
import ShowRecord from "@/components/ShowRecord.vue"; // Import ShowRecord component

export default {
  name: "HomeView",
  components: {
    NavBar,
    HeaderView,
    CropSearchBar,
    ShowRecord,
  },
  data() {
    return {
      records: [], // 保存 API 獲取的資料
    };
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    fetchData() {
      axios
        .get(
          "https://data.moa.gov.tw/Service/OpenData/FromM/FarmTransData.aspx?IsTransData=1&UnitId=037"
        )
        .then((response) => {
          this.records = response.data; // 將 API 資料儲存到 records
        })
        .catch((error) => {
          console.error("API error:", error);
        });
    },
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
