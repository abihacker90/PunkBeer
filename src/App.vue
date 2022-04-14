<script setup>

</script>


<template>
  <header>
    
      <h1>Punk Beer Collection</h1>
       <div class="searchBar">
      <input
        v-on:keypress.enter=""
        class=""
        v-model="search"
        type="text"
        placeholder="Search for beer name..."
      />
    </div>
      
  
  </header>

  <main>
    <div>
    <div id="container">
      <div v-for="beer in filterBeers" :key="beer.id" class="card">
        <div class="img">
          <img :src="beer.image_url" alt="Placeholder image" />
        </div>
        <div class="content">
          <h2>{{ beer.name }}</h2>
          <p>{{ beer.description }}</p>
        </div>
      </div>
    </div>
  </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      allBeers: [],
      search: "",
    };
  },
   mounted() {
    fetch("https://api.punkapi.com/v2/beers?page=1&per_page=80")
      .then((res) => res.json())
      .then((data) => (this.allBeers = data))
      .catch((err) => console.log(err.message));
  },
  computed: {
    filterBeers() {
      return this.allBeers.filter(beer =>
      beer.name.toLowerCase().includes(this.search.toLowerCase()))
    }
  }
};
</script>


<style>

#app {
  margin: 0;
  max-width: 100%;
  font-weight: normal;
}


header {
  display: block;
  position: relative;
  width: 100%;
  height: 35vh;
  background-image: url("./assets/Beer-Tube-Cover-ipad-air.jpg");
  background-position: center; 
  background-repeat: no-repeat;
  background-size: cover;
}

h1 {
  display: inline;
  color: #fff;
  background-color: #000;
  font-size: 3rem;
  margin: 0 0.5em;
  padding: .1em .2em;
}
.searchBar {
  width: 100%;
  position: absolute;
  bottom: 10px;
  align-items: center;
}
.searchBar input {
  width: 20%;
  padding: 10px;
  margin: auto;
  display: block;
  color: #fff;
}
input::placeholder{

  color: #fff;
  font-size: 1.2rem;
}
#container {
  width: 90%;
  height: auto;
  margin: auto;
  display: flex;
  flex-wrap: wrap;
}

.card {
  display: flex;
  width: 45%;
  height: auto;
  background: #888;
  margin: 20px;
  padding: 5px;
  border-radius: 7%;
  box-shadow: 5px 10px #333;
}
.card img {
  width: 75%;

}
.content {
  width: 40%;
}
.content h2 {
  font-size: 2.5rem;
  color: #fff;
  padding: 5px;
}
.content p {
  font-size: 1.2rem;
  padding: 5px;
  line-height: 1.5;
}
.img {
  width: 40%;
}

.card div {
  display: inline-block;
}

</style>
