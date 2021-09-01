<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm': ''">
    <main>
      <div class="search-box">
        <input 
          type="text" 
          name="" 
          id="" 
          class="search-bar" 
          placeholder="Search..."
          v-model="params"
          @keypress="fetchWeather"
        >
      </div>

      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{weather.name}}, {{weather.sys.country}}</div>
          <div class="date">{{ dateBuilder() }}</div>
        </div>

        <div class="weather-box">
          <div class="temperature">{{Math.round(weather.main.temp)}}°c</div>
          <div class="weather">{{weather.weather[0].main}}</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>

import './styles/global.css';

export default {
  name: 'App',
  data(){
    return{
      api_key: '248c3f60e5ca048898e57d5ec1df6822',
      base_url: `https://api.openweathermap.org/data/2.5/`,
      params: '',
      weather: { }
    }
  },
  methods:{
    fetchWeather(e){
      if(e.key === 'Enter'){
        fetch(`${this.base_url}weather?q=${this.params}&units=metric&APPID=${this.api_key}`)
        .then((res)=>{
          return res.json();
        })
        .then(this.setResults)
        .catch((err)=>{
          alert(`Failed to fetch data: ${err}`);
        })
      }
    },
    setResults(results){
      this.weather = results
    },
    dateBuilder(){
      let d = new Date();
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();

      return `${day} ${date} ${month} ${year}`;
    }
  }
}
</script>

<style>
#app{
  background-image: url('./assets/cold-bg.jpg');
  background-position: bottom;
  background-size: cover;
  transition: .4s;
}

#app.warm {
  background-image: url('./assets/warm-bg.jpg');
}

@media (min-width: 768px) {
  #app{
    background-repeat: no-repeat;
    background-position: top;
  }
}

main{
  min-height: 100vh;
  padding: 25px;

  background-image: linear-gradient(to bottom, var(--gradient-1), var(--gradient-2));
}

.search-box{
  width: 100%;
  margin-bottom: 30px;
}

.search-box .search-bar{
  display: block;
  width: 100%;
  padding: 15px;

  color: var(--text);
  font-size: 20px;

  appearance: none;
  border: none;
  outline: none;
  background: none;

  box-shadow: 0px 0px 16px var(--gradient-1);
  background: var(--background);
  border-radius: 0px 16px;
  transition: .4s;
}

.search-box .search-bar:focus{
  box-shadow: 0px 0px 16px var(--gradient-1);
  background: var(--background-active);
  border-radius: 16px 0px;
}

.location-box .location{
  color: var(--white);
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px var(--gradient-1);
}

.location-box .date{
  color: #fff;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}

.weather-box{
  text-align: center;
}

.weather-box .temperature{
  display: inline-block;
  padding: 10px 25px;
  color: var(--white);
  font-size: 102px;
  font-weight: 900;

  text-shadow: 3px 6px var(--gradient-1);
  background: var(--background);
  border-radius: 16px;
  margin: 30px 0;

  box-shadow: 3px 6px var(--gradient-1);
}

.weather-box .weather{
  color: var(--white);
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px var(--gradient-1);
}
</style>
