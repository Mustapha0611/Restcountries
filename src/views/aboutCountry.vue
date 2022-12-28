<template>
  <div class="about-country">
    <header :class="{headerWhite:lightMode}" >
      <nav>
        <h2 :class="{headerWhite:lightMode}"> Where in the world</h2>
        <section class="mode-toggle" @click="toggleMode">
          <div class="bg-changer" v-if="darkMode">
            <img src="@/assets/icon-sun.svg" alt=""/> <span :class="{headerWhite:lightMode}"> Light Mode </span>
          </div>
          <div class="bg-changer" v-if="lightMode">
            <img src="@/assets/icon-moon.svg" alt="" :class="{changebg:lightMode}"/> <span :class="{headerWhite:lightMode}">Dark Mode</span>
          </div>
        </section>
      </nav>
    </header>
    <div class="wrapper" :class="{lightwrapper:lightMode}">
      <section class="link">
        <router-link :to="{name:'home'}" class="link-child" :class="{lightlink:lightMode}"> <img src="@/assets/leftarrow.svg"  class="leftarrow" :class="{lightarrow:lightMode}" > Back</router-link>
      </section>
      <section class="main-content">
        <div class="flag">
          <img :src="country[0].flags.png" alt="" srcset=""> 
        </div>
        <div class="country-details">
          <h2 :class="{lightdetails:lightMode}">{{ name }}</h2>
          <section class="details">
            <p :class="{lightdetails:lightMode}"><strong :class="{lightdetails:lightMode}">Native Name: </strong> {{ country[0].nativeName }}</p>
            <p :class="{lightdetails:lightMode}"><strong :class="{lightdetails:lightMode}">Top Level Domain: </strong> {{ country[0].topLevelDomain[0] }}</p>
            <p :class="{lightdetails:lightMode}"><strong :class="{lightdetails:lightMode}">Population: </strong> {{country[0].population }}</p>
            <p :class="{lightdetails:lightMode}"><strong :class="{lightdetails:lightMode}">Currencies: </strong> {{ country[0].currencies[0].name }}</p>
            <p :class="{lightdetails:lightMode}"><strong :class="{lightdetails:lightMode}">Region: </strong> {{ country[0].region }}</p>
            <p :class="{lightdetails:lightMode}"><strong :class="{lightdetails:lightMode}">Languages: </strong> {{ country[0].languages[0].name }}</p>
            <p :class="{lightdetails:lightMode}"><strong :class="{lightdetails:lightMode}">Sub Region: </strong> {{country[0].subregion }}</p>
            <p :class="{lightdetails:lightMode}"><strong :class="{lightdetails:lightMode}">Capital: </strong>{{ country[0].capital }}</p>
          </section>
         <ul class="border-country">
            <strong :class="{lilight:lightMode}">Border Countries:</strong> <li v-for="count in country[0].borders" :class="{lilight:lightMode}" > {{ count }} </li>
          </ul> 
        </div>
      </section>
    </div>
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
      country:[],
      name:this.$route.params.name, 
    };
  },
  mounted(){
    axios.get(`https://restcountries.com/v2/name/${this.name}`)
    .then(resp=>{
      this.country = resp.data
      console.log(this.country)
    })
  },
  computed:{
  },
  methods: {
    toggleMode() {
      this.darkMode = !this.darkMode;
      this.lightMode = !this.lightMode;
    },
  },
};
</script>
<style scoped>
* {
  margin: 0;
  padding: 0;
  color:hsl(0, 0%, 100%);
  font-size:14px;
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
.wrapper{
  background-color: hsl(207, 26%, 17%);
  height: calc(100vh - 130px);
  padding:20px 0;
  
}
.lightwrapper{
  background-color: hsl(0, 0%, 100%);
  color:hsl(200, 15%, 8%)
}
.link-child{
  position:absolute;
  top:100px;
  left:1%;
  display: flex;
  justify-content: center;
  align-items: center;
  width:150px;
  margin:40px 5%;
  height:50px;
  text-decoration: none;
  background-color: hsl(209, 23%, 22%);
  box-shadow: 1px 2px 3px hsl(212, 79%, 13%);
  border-radius:5px;
}
.lightlink{
  background-color: hsl(0, 0%, 100%);
  color:hsl(212, 79%, 13%)
}
.leftarrow{
  margin:0 5px;
  width:15px;
  height:25px;
  filter: invert(98%) sepia(98%) saturate(8%) hue-rotate(162deg) brightness(102%) contrast(104%);
}
.lightarrow{
  filter: invert(0%) sepia(9%) saturate(7465%) hue-rotate(136deg) brightness(94%) contrast(107%);
}
.main-content{
  display:flex;
  /* border:1px solid white; */
  margin-top: 140px;
  margin-left:6%;
  height:400px;
  width:88%;
}
.flag{
  width:50%;
  box-shadow: 2px 2px 3px grey;
}
.flag img{
  width:100%;
  height:100%;
}
.country-details{
  width:50%;
  /* border:1px solid red; */
  padding:30px 10%;
}
.country-details  h2{
  font-size: 2.5rem;
  font-weight:600;
}
.details{
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-row-gap: 20px;
  width:100%;
  /* border:1px solid red; */
  margin:30px 0;
}
.lightdetails{
  color:hsl(200, 15%, 8%);
}
.border-country{
  margin-top:100px;
}
li{
  list-style: none;
  display:inline-block;
  margin:5px;
  border-radius:5px;
  box-shadow: 1px 2px 3px hsl(0, 100%, 4%);
  padding:5px 20px;
  background-color: hsl(209, 23%, 22%);
  font-weight:300;
}
.lilight{
  color:hsl(200, 15%, 8%);
  background-color: hsl(0, 0%, 100%);
}
@media  screen and (max-width:720px) {
  .main-content{
    flex-direction: column;
    height: auto;
  }
  .wrapper{
    height:auto;
  }
  .flag{
    width:100%;
    height:300px
  }
  .country-details{
  width:100%;
  padding:30px 3%;
}
.country-details  h2{
  font-size: 2.5rem;
  font-weight:600;
}
.details{
  display: grid;
  grid-template-columns: 1fr;
  grid-row-gap: 20px;
  width:100%;
  /* border:1px solid red; */
  margin:30px 0;
}
.border-country{
  margin-top:50px;
}
}
</style>

