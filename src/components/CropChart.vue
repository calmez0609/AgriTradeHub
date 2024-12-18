<template>
  <div class="container">
    <h2>作物交易量與價格圖</h2>
    <canvas id="cropChart"></canvas>
  </div>
</template>

<script>
// 引入 Chart.js 相關組件
import { Chart as ChartJS, 
         CategoryScale, 
         LinearScale, 
         LineElement, 
         PointElement, // 註冊 PointElement
         Title, 
         Tooltip, 
         Legend, 
         LineController 
       } from 'chart.js';

// 註冊需要的組件
ChartJS.register(
  CategoryScale,
  LinearScale,
  LineElement,
  PointElement, // 註冊 PointElement
  Title,
  Tooltip,
  Legend,
  LineController // 註冊 LineController
);

export default {
  name: "CropChart",
  props: {
    records: {
      type: Array,
      required: true,
    },
  },
  mounted() {
    this.renderChart();
  },
  methods: {
    renderChart() {
      const ctx = document.getElementById("cropChart").getContext("2d");

      new ChartJS(ctx, {
        type: "line", // 設置為折線圖
        data: {
          labels: this.records.map((record) => record['作物名稱']), // 使用作物名稱作為橫軸
          datasets: [
            {
              label: "交易量", // 顯示交易量
              data: this.records.map((record) => record['交易量']),
              borderColor: "rgba(75, 192, 192, 1)", // 交易量顏色
              backgroundColor: "rgba(75, 192, 192, 0.2)", // 透明背景
              fill: true, // 填充區域
            },
            {
              label: "上價", // 顯示上價
              data: this.records.map((record) => record['上價']),
              borderColor: "rgba(255, 99, 132, 1)", // 上價顏色
              backgroundColor: "rgba(255, 99, 132, 0.2)", // 透明背景
              fill: false, // 不填充區域
            },
            {
              label: "中價", // 顯示中價
              data: this.records.map((record) => record['中價']),
              borderColor: "rgba(255, 159, 64, 1)", // 中價顏色
              backgroundColor: "rgba(255, 159, 64, 0.2)", // 透明背景
              fill: false, // 不填充區域
            },
            {
              label: "下價", // 顯示下價
              data: this.records.map((record) => record['下價']),
              borderColor: "rgba(153, 102, 255, 1)", // 下價顏色
              backgroundColor: "rgba(153, 102, 255, 0.2)", // 透明背景
              fill: false, // 不填充區域
            }
          ]
        },
        options: {
          responsive: true, // 圖表自適應
          scales: {
            x: {
              title: {
                display: true,
                text: "作物名稱", // 用作物名稱為 x 軸標題
              }
            },
            y: {
              title: {
                display: true,
                text: "數值", // 用數值為 y 軸標題
              },
              beginAtZero: true, // 縱軸從 0 開始
            }
          },
          plugins: {
            legend: {
              position: "top", // 圖例顯示位置
            },
            tooltip: {
              callbacks: {
                label: function (tooltipItem) {
                  let label = tooltipItem.dataset.label || ''; // 取得dataset標籤
                  let value = tooltipItem.raw; // 取得數值

                  if (label === "交易量") {
                    return `${label}: ${value} 件`; // 交易量顯示 "件"
                  } else {
                    return `${label}: NT ${value} 元`; // 其他顯示為 "NT"
                  }
                }
              }
            }
          }
        }
      });
    }
  }
};
</script>

<style scoped>
.container {
  margin-top: 20px;
  text-align: center;
}
canvas {
  max-width: 100%;
  height: auto;
}
</style>
