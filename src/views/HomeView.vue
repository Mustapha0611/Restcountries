<template>
  <div class="home">
    <header :class="{headerWhite:lightMode}">
      <nav>
        <h2 :class="{headerWhite:lightMode}">Where in the world</h2>
        <section class="mode-toggle" @click="toggleMode" >
          <div class="bg-changer" v-if="darkMode">
            <img src="@/assets/icon-sun.svg" alt=""/> <span :class="{headerWhite:lightMode}"> Light Mode </span>
          </div>
          <div class="bg-changer" v-if="lightMode">
            <img src="@/assets/icon-moon.svg" alt="" :class="{changebg:lightMode}"/> <span :class="{headerWhite:lightMode}">Dark Mode</span>
          </div>
        </section>
      </nav>
    </header>
    <main class="container" :class="{containerlight:lightMode}">
      <div class="inputs">
        <div class="input">
          <label>
            <input
              v-model="search"
              type="search"
              placeholder="Search for a country..."
              class="input-text"
              :class="{inputlight:lightMode}"
            />
          </label>
        </div>
        <div class="filter">
          <select v-model="byRegion" name="region" class="select">
            <option value="" >Filter by Region</option>
            <option value="Africa">Africa</option>
            <option value="America">America</option>
            <option value="Asia">Asia</option>
            <option value="Europe">Europe</option>
            <option value="Oceania">Oceania</option>
          </select>
        </div>
      </div>
      <div class="items">
        <div v-for="country in filteredcountries" :key="country.id" class="item" :class="{itemlight:lightMode}">
          <router-link v-bind:to="{name:'about', params:{id:country.id}}"><img :src="country.flags.png" alt="" srcset=""></router-link>
          <section class="more-info"  :class="{moreinfolight:lightMode}" >
            <p class="country-name"  :class="{moreinfolight:lightMode}">{{country.name}}</p>
            <p><span :class="{moreinfolight:lightMode}">Population: {{country.population}}</span></p>
            <p><span :class="{moreinfolight:lightMode}">Region: {{country.region}}</span></p>
            <p><span :class="{moreinfolight:lightMode}">Capital: {{country.capital}}</span></p>
          </section>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: "HomeView",
  data() {
    return {
      darkMode: true,
      lightMode: false,
      search:'',
      byRegion:'',
      countries:[]
    };
  },
  mounted(){
    axios.get('https://restcountries.com/v2/all')
    .then(resp=>{
      this.countries = resp.data
    })
  },
  computed:{
    filteredcountries: function(){
      return this.countries.filter(count=>{
        return count.name.match(this.search) && count.region.match(this.byRegion)
      })
    },

  },
  methods: {
    toggleMode() {
      this.darkMode = !this.darkMode;
      this.lightMode = !this.lightMode;
    },
  },
};
</script>
<style>
* {
  margin: 0;
  padding: 0;
  color:hsl(0, 0%, 100%);
}
header {
  height: 90px;
  background: hsl(209, 23%, 22%);
  display: flex;
  padding: 0 5%;
  align-items: center;
  color: hsl(0, 0%, 100%);
  box-shadow: 0px 5px 5px hsl(0, 100%, 4%);
  transition: all .3s;
}
.headerWhite{
  background-color: hsl(0, 0%, 98%);
  color:hsl(200, 15%, 8%);
}
.bg-changer {
  position: absolute;
  right: 5%;
  top: 30px;
  cursor: pointer;
  display: flex;
  align-items: center;
}
.bg-changer > img {
  width: 20px;
  height: 20px;
}
.changebg{
  filter:invert(3%) sepia(51%) saturate(100%) hue-rotate(223deg) brightness(0) contrast(102%);
}
.mode-toggle > div > span {
  margin: 5px;
}
.container {
  height:auto;
  background-color: hsl(207, 26%, 17%);
  transition: all .3s;
}
.containerlight{
  background-color: hsl(0, 0%, 98%);
}
.inputs {
  display: flex;
}
.input {
  position: relative;
  width: 100%;
  margin: 0;
  /* padding: 0 12px; */
}
label {
  width: 100%;
  margin: 0;
  padding: 0;
}
 .input-text {
  width: 500px;
  margin: 20px 7%;
  background: hsl(209, 23%, 22%);
  border: none;
  outline: none;
  color: #fff;
  padding: 17px 5em;
  background-image: url("../assets/icon-search.svg");
  background-position-y: center;
  background-position-x: 5%;
  background-size: 20px;
  background-repeat: no-repeat;
  border-radius: 3px;
}
.inputlight{
  background-color:hsl(0, 0%, 98%) ;
  box-shadow: 2px 3px 3px 2px rgb(199, 199, 199);
  color: hsl(0, 0%, 52%);
  background-image: url("../assets/icons8-search-50.png");
  background-size: 20px;
}
 .filter{ 
    margin: 20px 5%;
    } 
.select{
  width: 200px;
  height: 50px;
  border:none;
  outline:none;
  padding: 10px 15px;
  color: hsl(0, 0%, 100%);
  background-color: hsl(209, 23%, 22%);
}

.items{
  display:grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  padding:10px 4%;
  /* outline: 1px solid red; */
}
.item{
  background-color: hsl(209, 23%, 22%);
  height:400px;
  margin:30px 5%;
}
.itemlight{
  background:hsl(0, 0%, 98%);
  box-shadow: 2px 2px 2px 3px rgb(238, 238, 238);
  
}
.item img{
  width:100%;
  height:200px;
}
.more-info{
 padding: 0px 7%;
 }
 .moreinfolight{
  color:hsl(200, 15%, 8%);
 }
 .country-name{
  font-size: 18px;
  font-weight: 600;
  margin: 20px 0;
 }
</style>
