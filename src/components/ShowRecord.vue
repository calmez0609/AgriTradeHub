<template>
    <div class="container">
      <h2>交易紀錄</h2>
      <table class="table table-striped">
        <thead>
          <tr>
            <th>交易日期</th>
            <th>作物名稱</th>
            <th>市場名稱</th>
            <th>上價</th>
            <th>中價</th>
            <th>下價</th>
            <th>平均價</th>
            <th>交易量</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(record, index) in records.slice(0, 10)" :key="index">
            <td>{{ record['交易日期'] }}</td>
            <td>{{ record['作物名稱'] }}</td>
            <td>{{ record['市場名稱'] }}</td>
            <td>{{ record['上價'] }}</td>
            <td>{{ record['中價'] }}</td>
            <td>{{ record['下價'] }}</td>
            <td>{{ record['平均價'] }}</td>
            <td>{{ record['交易量'] }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    name: "ShowRecord",
    props: {
      records: {
        type: Array,
        required: true,
      },
    },
  };
  </script>
  <style scoped>
  /* 可加上您自己需要的樣式 */
  table {
    width: 100%;
    margin-top: 20px;
  }
  th, td {
    text-align: center;
  }
  </style>
  