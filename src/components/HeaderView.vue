<template>
  <div
    class="jumbotron appHidden"
    style="background-image: url(https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRC7dlAZsU-828u8yWt0XVInwk0Fq-DdITZag&s); background-size: cover; background-repeat: no-repeat; background-position: center;"
  >
    <div class="container px-0">
      <ol class="breadcrumb">
        <li class="breadcrumb-item">
          <em class="fas fa-home"></em>
          <a>{{ Headermsg }}</a>
        </li>
      </ol>
      <h2 id="content">
        <em class="far fa-newspaper fa-icon"></em>&nbsp;{{ Titlemsg }}
      </h2>
    </div>
  </div>
</template>

<script>
export default {
  name: "HeaderView",
  data() {
    return {
      Headermsg: "首頁",
      Titlemsg: "文心蘭",
    };
  },
};
</script>

<style scoped>
.jumbotron {
  color: white;
  padding: 2rem 1rem;
  position: relative;
}

.breadcrumb {
  background: transparent;
  padding: 0;
  margin-bottom: 1rem;
}

.breadcrumb-item a {
  color: white;
  text-decoration: none;
}

.breadcrumb-item a:hover {
  text-decoration: underline;
}

h2 {
  color: white;
  font-size: 2rem;
  font-weight: bold;
  margin: 0;
}

.fa-icon {
  width: 80px;
  height: 80px;
  display: inline-block;
  text-align: center;
  line-height: 80px;
  font-size: 2rem;
  color: black;
  vertical-align: middle;
}

a {
  color: white;
  font-size: 2rem;
  font-weight: bold;
  margin: 0;
}
</style>