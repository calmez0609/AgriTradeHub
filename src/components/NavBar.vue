<template>
    <nav class="navbar">
      <div class="logo">AgriTradeHub</div>
      <ul class="nav-links">
        <li><router-link to="/Home">首頁</router-link></li>
      </ul>
    </nav>
  </template>
  
  <script>
  export default {
    name: "NavBar",
  };
  </script>
  
  <style scoped>
  .navbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem 2rem;
    background-color: #4caf50;
    color: white;
    width: 100%;
    margin: 0;
  }
  
  .logo {
    font-size: 1.5rem;
    font-weight: bold;
    white-space: nowrap;
  }
  
  .nav-links {
    list-style: none;
    display: flex;
    gap: 1.5rem;
    margin: 0;
    padding: 0;
  }
  
  .nav-links li {
    margin: 0;
  }
  
  .nav-links li a {
    text-decoration: none;
    color: white;
    font-weight: bold;
    transition: color 0.3s ease;
  }
  
  .nav-links li a:hover {
    color: #c8e6c9;
  }
  
  .nav-links li a.router-link-active {
    text-decoration: underline;
    color: #ffffff;
  }
  </style>
  