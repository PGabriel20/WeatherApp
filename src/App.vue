<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input type="text" name="" id="" class="search-bar" placeholder="Search...">
      </div>

      <div class="weather-wrap">
        <div class="location-box">
          <div class="location">London, UK</div>
          <div class="date">Wednsday 20 September 2021</div>
        </div>

        <div class="weather-box">
          <div class="temperature">9°c</div>
          <div class="weather">Rain</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return{
      api_key: '248c3f60e5ca048898e57d5ec1df6822',

    }
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body{
  font-family: 'montserrat', sans-serif;
}

#app{
  background-image: url('./assets/cold-bg.jpg');
  background-position: bottom;
  background-size: cover;
  transition: .4s;
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

  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));
}

.search-box{
  width: 100%;
  margin-bottom: 30px;
}

.search-box .search-bar{
  display: block;
  width: 100%;
  padding: 15px;

  color: #313131;
  font-size: 20px;

  appearance: none;
  border: none;
  outline: none;
  background: none;

  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background: rgba(255, 255, 255, 0.5);
  border-radius: 0px 16px;
  transition: .4s;
}

.search-box .search-bar:focus{
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0px;
}

</style>
