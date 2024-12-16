<template>
  <div class="container">
    <div class="row">
      <div class="col-12 mobile-font">
        <div class="form-row search_bar">
          <!-- 第一行: 依作物類別、交易市場、依作物 -->
          <div class="form-group col-lg-4 col-md-4 col-12">
            <label for="ddlCropCategory">依作物類別</label>
            <div class="form-row" style="padding-left: 5px; padding-right: 5px;">
              <select
                class="custom-select"
                v-model="selectedCropCategory"
                id="ddlCropCategory"
                name="TcType"
              >
                <option value="-1" selected>選擇作物類別</option>
                <option value="N04">蔬菜</option>
                <option value="N05">果品</option>
                <option value="N06">花卉</option>
              </select>
            </div>
          </div>

          <div class="form-group col-lg-4 col-md-4 col-12">
            <label for="MarketId">交易市場</label>
            <div class="form-row" style="padding-left: 5px; padding-right: 5px;">
              <button class="btn btn-outline-secondary" @click="toggleDropdown">
                選擇交易市場
              </button>

              <!-- Dropdown menu for market selection -->
              <div v-if="dropdownVisible" class="dropdown-menu show" style="position: absolute; z-index: 1000; width: 200px;">
                <div v-for="market in markets" :key="market.value" class="dropdown-item">
                  <input
                    type="checkbox"
                    :id="'market-' + market.value"
                    :value="market.value"
                    v-model="selectedMarkets"
                  />
                  <label :for="'market-' + market.value">{{ market.label }}</label>
                </div>
              </div>
            </div>
          </div>

          <div class="form-group col-lg-4 col-md-4 col-12">
            <label for="CropName">依作物</label>
            <div class="form-row">
              <div class="form-group col CropName">
                <button
                  type="button"
                  id="btnChooseCrop"
                  class="btn btn-light form-control exclude"
                  @click="openCropModal"
                >
                  {{ selectedCrop ? selectedCrop : '請選擇' }}
                </button>
              </div>
              <div
                id="CropNameList"
                v-if="selectedCropList.length"
                class="text-truncate form-group col border rounded bg-white form-control m-0 mx-1"
              >
                <span v-for="crop in selectedCropList" :key="crop" class="badge badge-secondary">
                  {{ crop }}
                </span>
              </div>
            </div>
          </div>
        </div>

        <!-- 第二行: 關鍵字查詢、日期區間、搜尋和列出全部按鈕 -->
        <div class="form-row search_bar">
          <!-- Keyword Search -->
          <div class="form-group col-lg-4 col-md-5 col-12">
            <label for="ByKeyword">關鍵字或代號查詢</label>
            <div class="input-group">
              <input
                type="text"
                v-model="keyword"
                class="form-control"
                placeholder="鳳梨、B4"
                id="ByKeyword"
                name="ByKeyword"
              />
              <div class="input-group-append">
                <button type="button" class="btn mt-0 btn-light border voiceInput">
                  <em class="fas fa-microphone"></em>
                </button>
              </div>
            </div>
            <label>請勿輸入特殊字元（標點符號及空格）</label>
            <span id="spKeywordDesc">輸入名稱或代號，例如：鳳梨、B4</span>
          </div>

          <!-- Date Range -->
          <div class="form-group col-lg-4 col-md-3 col-12">
            <label for="DateRange">交易日期區間</label>
            <div class="form-row date-picker">
              <input
                type="date"
                v-model="startDate"
                id="startDate"
                class="form-control"
                :max="endDate"
              />
              <input
                type="date"
                v-model="endDate"
                id="endDate"
                class="form-control"
                :min="startDate"
              />
            </div>
          </div>

          <!-- Search and Reset Buttons -->
          <div class="col-lg-2 col-md-2 col-6">
            <input type="hidden" v-model="cropId" />
            <button type="button" class="btn mb-2 form-control btnQuery" @click="search">
              <em class="fa fa-search"></em> 搜尋
            </button>
          </div>
          <div class="col-lg-2 col-md-2 col-6">
            <button type="button" class="btn mb-2 form-control btnQueryAll" @click="listAll">
              列出全部
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import '@/css/CropSearchBar.css'; // 引入外部 CSS 檔案

export default {
  data() {
    return {
      selectedCropCategory: '-1',
      selectedMarkets: ['514'], // Default selected market
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
  },
};
</script>
