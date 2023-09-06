<script>
export default {
  name: "App",
  data() {
    return {
      title: "Welcome to Opportunity",
      /* sheet_id: import.meta.env.VITE_GOOGLE_SHEET_ID,
      api_token: import.meta.env.VITE_GOOGLE_API_KEY, */
    };
  },
};

const tasks = [
  {
    taskName: "Personal Marketing Workshop",
    taskTime: "15:00",  
    taskAdress: "Räffelstrasse 12, 8046 Zürich",
    },
    
    {
    taskName: "Personal Marketing Workshop",
    taskTime: "15:00",  
    taskAdress: "Räffelstrasse 12, 8046 Zürich",
    },
    
    {
      taskName: "Personal Marketing Workshop",
    taskTime: "15:00",  
    taskAdress: "Räffelstrasse 12, 8046 Zürich",
    }
  ];

  function 

</script>
<template>
  <div id="app">
    
    <div>
      <h1 class="site-title">{{ title }}</h1>
    </div>

    <div>
        <h1>Date </h1>
    </div>

  </div>



</template>
<style>
#app {
  font-family: "Inter", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #323d4a;
  margin: 60px;
}
</style>
