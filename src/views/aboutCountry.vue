<template>
  <div class="about-country">
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
    <div class="wrapper">
      <section class="link">
        <router-link :to="{name:'home'}" class="link-child"> <img src="@/assets/leftarrow.svg" class="leftarrow"> Back</router-link>
      </section>
      <section class="main-content">
        <div class="flag">

        </div>
        <div class="country-details">

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
      countries:[],
      Id:this.$route.params.id, 
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
<style scoped>
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
.wrapper{
  background-color: hsl(207, 26%, 17%);
  height: calc(100vh - 90px);
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
  box-shadow: 2px 2px 2px 2px hsl(212, 79%, 13%);
  border-radius:5px;
}
.leftarrow{
  margin:0 5px;
  width:15px;
  height:25px;
  filter: invert(98%) sepia(98%) saturate(8%) hue-rotate(162deg) brightness(102%) contrast(104%);
}
</style>

