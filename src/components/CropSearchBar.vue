<template>
  <div class="crop-search-bar">
    <!-- 搜尋欄容器 -->
    <div class="search-container">
      <!-- 依作物類別 -->
      <div class="field">
        <label for="category">依作物類別</label>
        <select id="category" v-model="selectedCategory" @change=" loadMarkets">
          <option value="vegetable">蔬菜</option>
          <option value="fruit">水果</option>
          <option value="pottedflowers">盆花</option>
          <option value="flower">花卉</option>
        </select>
      </div>

      <!-- 交易市場 -->
        <div class="field">
          <label for="market">交易市場</label>
          <select id="market" v-model="selectedMarkets" :disabled="!selectedCategory">
            <option disabled value="">請先選擇作物類別</option>
            <option v-for="market in markets" :key="market.value" :value="market.value">
        {{ market.label }}
            </option>
        </select>
      </div>

      <!-- 依作物 -->
      <div class="field">
        <label for="crop">依作物</label>
        <input type="text" id="crop" placeholder="請選擇" />
      </div>

      <!-- 換行：第二行 -->
      <div class="field wide">
        <label for="search">關鍵字或代號查詢</label>
        <div class="input-group">
          <input type="text" id="search" placeholder="鳳梨、B4" />
          <button class="mic-button">🎤</button>
        </div>
        <small>請勿輸入特殊字元（標點符號及空格）</small>
      </div>

      <!-- 交易日期區間 -->
      <div class="field date">
        <label>交易日期區間</label>
        <div class="date-picker">
          <input type="date" />
          <input type="date" />
        </div>
      </div>

      <!-- 按鈕區 -->
      <div class="buttons">
        <button class="search-button">🔍 搜尋</button>
        <button class="list-all-button">列出全部</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.crop-search-bar {
  background-color: #0a6b5c;
  padding: 20px;
  color: white;
  border-radius: 8px;
  font-family: Arial, sans-serif;
  display: flex;
  justify-content: center; /* 水平置中 */
}

.search-container {
  display: flex;
  flex-wrap: wrap; /* 換行 */
  justify-content: center; /* 水平置中 */
  gap: 20px 30px; /* 上下和左右間隔 */
  max-width: 900px; /* 最大寬度，防止過寬 */
  width: 100%; /* 讓內容自適應寬度 */
}

.field {
  display: flex;
  flex-direction: column;
  flex: 1 1 200px; /* 欄位最小寬度200px */
  text-align: left;
}

.field label {
  margin-bottom: 5px;
  font-size: 14px;
}

.field select,
.field input {
  padding: 5px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.field.wide {
  flex: 1 1 100%; /* 關鍵字查詢框獨占一行 */
}

.input-group {
  display: flex;
}

.input-group input {
  flex: 1;
}

.mic-button {
  margin-left: 5px;
  border: none;
  background-color: #f0f0f0;
  cursor: pointer;
  border-radius: 4px;
  padding: 5px 10px;
}

.field.date .date-picker {
  display: flex;
  gap: 10px;
}

.date-picker input {
  width: 100%;
}

.buttons {
  display: flex;
  gap: 10px;
  justify-content: center; /* 讓按鈕置中 */
  flex: 1 1 100%; /* 按鈕獨占一行 */
}

.search-button,
.list-all-button {
  padding: 8px 15px;
  font-size: 14px;
  color: #fff;
  background-color: #005f56;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.list-all-button {
  background-color: #444;
}

.search-button:hover,
.list-all-button:hover {
  background-color: #333;
}
</style>

<script>
import '@/css/CropSearchBar.css'; // 引入外部 CSS 檔案

export default {
  data() {
    return {
      selectedCategory:'',
      selectedMarkets: '', // Default selected market
      selectedCropList: [],
      selectedCrop: null,
      keyword: '',
      startDate: '2024-11-16',
      endDate: '2024-12-16',
      cropId: '',
      dropdownVisible: false, 
      markets: [
        { value: '104', label: '台北二' },
        { value: '109', label: '台北一' },
        { value: '220', label: '板橋區' },
        { value: '241', label: '三重區' },
        { value: '260', label: '宜蘭市' },
        { value: '338', label: '桃農' },
        { value: '400', label: '台中市' },
        { value: '420', label: '豐原區' },
        { value: '512', label: '永靖鄉' },
        { value: '514', label: '溪湖鎮' },
        { value: '540', label: '南投市' },
        { value: '648', label: '西螺鎮' },
        { value: '800', label: '高雄市' },
        { value: '830', label: '鳳山區' },
        { value: '900', label: '屏東市' },
        { value: '930', label: '台東市' },
        { value: '950', label: '花蓮市' },
      ],
    };
  },
  methods: {
    openCropModal() {
      // Logic to open crop selection modal (not implemented here)
      console.log('Opening crop selection modal');
    },
    search() {
      // Logic for searching based on selected filters
      console.log('Searching with:', {
        cropCategory: this.selectedCropCategory,
        markets: this.selectedMarkets,
        crops: this.selectedCropList,
        keyword: this.keyword,
        startDate: this.startDate,
        endDate: this.endDate,
      });
    },
    listAll() {
      // Logic for showing all items (reset filters)
      console.log('Listing all items');
      this.selectedCropCategory = '-1';
      this.selectedMarkets = [];
      this.selectedCropList = [];
      this.keyword = '';
      this.startDate = '2024-11-16';
      this.endDate = '2024-12-16';
    },
    toggleDropdown() {
      this.dropdownVisible = !this.dropdownVisible; // 切換下拉式選單顯示狀態
    },
     // 加載市場選項
     loadMarkets() {
  if (this.selectedCategory) {
    // 根據 selectedCategory 來篩選市場 (未來可根據需要擴展篩選條件)
    this.filteredMarkets = this.markets; // 假設未來 markets 會根據 category 篩選

    // 自動將交易市場設置為陣列中的第一個值
    if (this.filteredMarkets.length > 0) {
      this.selectedMarkets = this.filteredMarkets[0].value;
    } else {
      this.selectedMarkets = ''; // 若沒有符合的市場則設為空值
    }
  } else {
    // 重置市場和選擇值
    this.filteredMarkets = [];
    this.selectedMarkets = '';
  }
  },
 }
}
</script>