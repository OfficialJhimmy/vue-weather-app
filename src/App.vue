<template>
  <div id="app">
    <header>
      <a href="#" class="logo u-justify-content">WETTER</a>
    </header>

    <div class="container u-display-flex">
      <div class="container-content">
        <div class="banner u-display-flex-2 u-m-bottom">
          <h3>Weather App</h3>
          <h3>Its a great day today 👋</h3>
        </div>
        <div class="body-weather">
          <p class="u-m-bottom">
            WETTER is a Weather App for checking the current Weather condition
            for a particular City around the world.
          </p>
          <input
            type="search"
            placeholder="Enter a City..."
            v-model="query"
            name="searchWeather"
            id="weatherid"
          />
          <button @click="searchClick" class="button-weather">
            Check Weather
          </button>

          <div v-if="loading">
            <p>Loading...</p>
          </div>

          <div v-if="info.cod == 404">
            <h3>
              Oh No! not a valid City, please enter a valid location in the
              world 😊
            </h3>
          </div>

          <div v-if="info.cod != undefined && loading == false">
            <div v-if="this.info.main != undefined">
              <h4>{{ Math.round(info.main.temp) }} <span>°C</span></h4>
              <h4>{{ info.weather[0].main }}</h4>
              <div>
                <img src="http://openweathermap.org/img/wn/10d@2x.png" alt="" />
              </div>
              <h3>{{ info.name }}, {{ info.sys.country }}</h3>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      query: "",
      loading: false,
      url: "",
      info: {},
      location: "lagos,Nigeria",
      api_key: "066406f5de7a4d93834e44a9e015ebc6",
      base_url: "https://api.openweathermap.org/data/2.5/",
    };
  },
  methods: {
    // @keypress = 'search'
    // search(e) {
    //   if (e.key == "Enter") {
    //     this.loading = true;
    //     setTimeout(() => {
    //       this.loading = false;
    //     }, 1000);
    //     setTimeout(() => {
    //       fetch(
    //         `${this.base_url}weather?q=${this.query}&units=metric&appid=${this.api_key}`
    //       )
    //         .then(response => {
    //           response.json();
    //         })
    //         .then(this.results);
    //     }, 1000);
    //   }
    // },

    searchClick() {
      this.loading = true;
      setTimeout(() => {
        this.loading = false;
      }, 1000);
      setTimeout(() => {
        fetch(
          `${this.base_url}weather?q=${this.query}&units=metric&appid=${this.api_key}`
        )
          .then((response) => response.json())
          .then(this.results);
      }, 1000);
    },

    results(result) {
      this.info = result;
      this.url = `http://openweathermap.org/img/wn/${this.info.weather[0].icon}@2x.png`;
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Nunito:wght@200;400;600;700&family=Shalimar&display=swap");

@import "./index.css";

.u-justify-content {
  display: flex;
  justify-content: center;
}

.u-display-flex {
  display: flex;
  align-items: center;
  justify-content: center;
}

.u-display-flex-2 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.u-m-bottom {
  margin-bottom: 20px;
}

.container {
  height: 70vh;
  width: 100%;
  text-align: center;
}

.logo {
  font-family: "Shalimar", cursive;
  font-size: 3em;
  text-decoration: none;
  color: #333;
  margin-top: 30px;
}

input[type="search"] {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  font-family: inherit;
  margin: 10px 0;
  border: none;
  outline: none;
  resize: none;
  border-radius: 5px;
}

.button-weather {
  background-color: #00bcd4;
  border: none;
  font-size: 15px;
  padding: 10px;
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  margin: 20px 0;
  border-radius: 5px;
  color: #333;
  font-weight: 700;
  font-family: inherit;
}

@media screen and (max-width: 680px) {
  .u-justify-content {
    display: flex;
    justify-content: center;
  }

  .u-display-flex {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .u-display-flex-2 {
    display: block;
  }

  .u-m-bottom {
    margin-bottom: 14px;
  }

  h3 {
    font-size: 17px;
  }

  p {
    font-size: 14px;
    font-weight: 500;
  }

  .container {
    height: 80vh;
    padding: 20px 20px 0 20px;
  }

  .logo {
    font-size: 2em;
    margin-top: 20px;
  }

  input[type="search"] {
    width: 60%;
    padding: 10px;
    font-size: 14px;
    margin: 10px 0;
  }

  .button-weather {
    font-size: 14px;
    padding: 10px;
    margin: 13px 0;
    font-weight: 700;
  }
}
</style>
