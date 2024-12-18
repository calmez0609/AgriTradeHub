<template>
  <div class="home">
    <NavBar /> <!-- 引入 NavBar 組件 -->
    <HeaderView /> <!-- 引入 HeaderView 組件 -->
    <div class="content">
      <CropSearchBar />
    </div>
    <!-- 傳遞 API 資料給 ShowRecord 組件 -->
    <ShowRecord :records="topTenRecords" />
    <!-- 傳遞資料給 CropChart 組件 -->
    <CropChart :records="topTenRecords" />
  </div>
</template>

<script>
import axios from "axios";
import NavBar from "@/components/NavBar.vue";
import HeaderView from "@/components/HeaderView.vue";
import CropSearchBar from "@/components/CropSearchBar.vue";
import ShowRecord from "@/components/ShowRecord.vue"; // 引入 ShowRecord 組件
import CropChart from "@/components/CropChart.vue"; // 引入 CropChart 組件

export default {
  name: "HomeView",
  components: {
    NavBar,
    HeaderView,
    CropSearchBar,
    ShowRecord,
    CropChart, // 註冊 CropChart 組件
  },
  data() {
    return {
      records: [], // 保存 API 獲取的資料
    };
  },
  computed: {
    // 只取前 10 筆資料
    topTenRecords() {
      console.log(this.records.slice(0, 10))
      return this.records.slice(0, 10);
    }
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
