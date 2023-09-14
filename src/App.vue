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
      timeInterval: null, // Initializes time interval to null.   
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

      refreshData() {
      // Set up an interval to refresh data every 30 seconds
      setInterval(() => {
        this.getData();
      }, 30000); // 30 seconds in milliseconds
      console.log("Data refresh interval started"); // Log a message when the interval is started
    },

    stopDataRefresh() {
      // Clear the interval when the component is destroyed
      clearInterval(this.timeInterval);
      console.log("Data refresh interval stopped"); // Log a message when the interval is stopped

    }, 
  },

    mounted() {
    this.getData(); // get first initial data and then wait for the next update
    this.refreshData(); // start refresh data interval. 
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

    <div class="wrapper" >
        <div v-if="entries.length > 0" v-for="data in entries" class="card">
            <p class="card-time">{{ data[0] }}</p>
            <p class="card-title">{{ data[2] }}</p>
            <p class="card-description">{{ data[3] }}</p>
        </div>

        <div v-else>
          <h1 class="site-title">No tasks for today</h1>
        </div>
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
  color: #323d4a;
  max-width: 960px;
  margin-left: auto;
  margin-right: auto;
}

.site-title {
color: rgba(50, 61, 74, 1);
font-family: "Inter", Helvetica, Arial, sans-serif;
font-size: 62px;
font-weight: 900;
letter-spacing: 0em;
text-align: left;

}

.date h2 {
  color: rgba(154, 167, 177, 1);
  font-family: "Inter", Helvetica, Arial, sans-serif;
  font-size: 62px;
  font-weight: 500;
  text-align: left;
  margin-bottom: 12px;
  margin-top: 12px; 

}

.card {
  display: flexbox; 
  background-color: rgba(15, 5, 160, 1);
  font-family: "Inter", Helvetica, Arial, sans-serif;
  height: auto;
  margin-top: 50px;
  margin-bottom: 50px;  
  padding: 30px;
  line-height: 20px;
}

.wrapper {
  margin-bottom: 120px;
}

.card-time{
  color:rgba(235, 94, 0, 1);
  font-weight: bold;
  font-family: "Inter", Helvetica, Arial, sans-serif;
  font-size: 28px;
  font-weight: 900;
  text-align: left;
}

.card-title {
  color:rgba(255, 191, 171, 1);
  font-weight: 900;
  font-family: "Inter", Helvetica, Arial, sans-serif;
  font-size: 28px;
  text-align: left;
}

.card-description {
    font-size: 28px;
    color:rgba(255, 191, 171, 1);
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
  flex-wrap: wrap;
}

.logopic {
  width: 200px;
  height: 50px;
  margin: 10px;
}

body {
  background-color: rgba(232, 239, 244, 1);
  margin: 0px; 
}

/* @media only screen and (max-width: 850px){
  body  {
    background-color: brown;
  }
  .card {
    padding: 0px; 
  }
} */

    
</style>
