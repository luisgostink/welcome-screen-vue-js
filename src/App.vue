<script>
export default {
  name: "App",
  data() {
    return {
      title: "Welcome to Opportunity",
      date: new Date().toLocaleDateString('en-GB').replace(/\//g, '.'),
      sheet_id: import.meta.env.VITE_GOOGLE_SHEET_ID,
      api_token: import.meta.env.VITE_GOOGLE_API_KEY, 
      entries: [],
      currentDate: "",
      timeInterval: "",  
    };
  },
  computed: {
    // computed properties are like data properties, but with a method combined and it gets executed automatically, instead of calling a function explicitly.  
      gsheet_url() {
      return `https://sheets.googleapis.com/v4/spreadsheets/${this.sheet_id}/values:batchGet?ranges=A2%3AE100&valueRenderOption=FORMATTED_VALUE&key=${this.api_token}
      `;
      },
    },
    methods: {
    async getData() {
      const response = await fetch(this.gsheet_url);
      const data = await response.json();
      this.entries = data.valueRanges[0].values;
      console.log(this.entries); 
      },
    }, 
    mounted() {
    this.getData(); // get first initial data and then wait for the next update
  },
  }


</script>
<template>
  <div id="application">
    <div>
      <h1 class="site-title">{{ title }}</h1>
    </div>
    <div class="date">
      <h2>{{ date }}</h2>
    </div>

    <div v-for="data in entries" class="card">
        <p class="card-time">{{data[0]}}</p>
        <p>{{ data[1] }}</p> 
        <p class="card-title">{{ data[2] }}</p>
        <p class="card-description">{{ data[3] }}</p>
    </div>



  
  </div>

  <footer class="footer">
      <div class="logos">
          <img class="logopic" src="./assets/STZH_SEB_Logo.png">
          <img class="logopic" src="./assets/Opportunity.png">
          <img class="logopic" src="./assets/SAG_Logo_De.png">
      </div>
    </footer>



</template>

<style>

#application {
  font-family: "Inter", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 60px;
  color: #323d4a;
}

.card {
  display: flexbox; 
  background-color: darkblue;
  padding: 20px 50px 20px 50px; 
  font-weight: bold;
  font-size: 40px;
  font-family: "Inter", Helvetica, Arial, sans-serif;
  border-radius: 10px;
  margin-top: 60px;
  margin-bottom: 60px;
}

.card-time{
  color: red;
  font-weight: bold;
}

.card-title {
  color: orange;
  font-weight: bold;
}

.card-description {
    font-size: 20px;
    color: bisque;
}

.footer {
  position: fixed;
  bottom: 0;
  width: 100%;
  height: 70px;
  background-color: white;
  flex-direction: row;
}

.logos {
  display: flex;
  justify-content: space-around;
}

.logopic {
  width: 200px;
  height: 50px;
  margin: 10px;
}

body {
  background-color: lightcyan;
}

@media only screen and (max-width: 850px){
  body  {
    background-color: brown;
  }
  .card {
    padding: 0px; 
  }
}

    
</style>
