<template>
<div class="">
<nav class="navbar  navbar-expand-lg navbar-light bg-light fixed-top">
  <a class="navbar-brand" href="/">Beers</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>

  <div class="collapse navbar-collapse" id="navbarSupportedContent">
    <ul class="navbar-nav mr-auto">
      <li class="nav-item active">
        <a class="nav-link" href="/">Home <span class="sr-only">(current)</span></a>
      </li>
      
      <li class="nav-item dropdown">
        <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
          More info
        </a>
        <div class="dropdown-menu" aria-labelledby="navbarDropdown">
          <a class="dropdown-item" href="#">Action</a>
          <a class="dropdown-item" href="#">Another action</a>
          <div class="dropdown-divider"></div>
          <a class="dropdown-item" href="#">Something else here</a>
        </div>
      </li>
       
    </ul>
    <form class="form-inline my-2 my-lg-0">
      <input class="form-control mr-sm-2" type="search" placeholder="search beer ..." aria-label="Search">
      <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
    </form>
  </div>
</nav>
<div class="jumbotron">
  <div class="hello">
   <h1>{{msg}}</h1>
  </div>   
  </div>
  <div class="allmovies">
    <div class="container">
        <div class="row">
           <div class="col-md-6">
              <ul v-if="beers && beers.length">
                
                  <li v-for="beer of beers">
                  
                  <div class="card">
                  <div class="card-img-top beers-image">
                  <img :src="beer.image_url" />
                  </div>                                                             
                  <a href=""> <h4>{{beer.name}}</h4> </a>
                  <p><i>tags</i>: {{beer.tagline}}</p> 
                  <p>first_brewed: {{beer.first_brewed}}</p> 
                  <p>{{beer.description}}</p> 
                  <p>abv: {{beer.abv}}</p> 
                  <p>ibu: {{beer.ibu}}</p> 
                  <p>target_fg: {{beer.target_fg}}</p>
                  <p>target_og: {{beer.target_og}}</p> 
                  <p>ebc: {{beer.ebc}}</p> 
                  <p>srm: {{beer.srm}}</p> 
                  <p>ph: {{beer.ph}}</p> 
                  <p>attenuation_level: {{beer.attenuation_level}}</p>  
                 
                  </div>
                </li> 
                   
              </ul>

           </div>
           <div class="col-md-6">
 
               <ul v-if="beers && beers.length">
                
                  <li v-for="beer of beers">
                  
                  <div class="card sidebar">
                  <div class="card-img-top beers-image">
                   <img :src="beer.image_url" /> 
                  </div>                                                             
                  
                  </div>
                </li> 
                   
              </ul>
           </div>
             </div>
        <ul v-if="errors && errors.length">
          <li v-for="error of errors">
          {{error.message}}
          </li>
        </uL>
     
   
  </div>
  </div>
</div>
</template>

<script>
import axios from 'axios';

export default {
 
  data() {
    return {
      msg: "Find your favorite Beers ",
      beers:[],
      errors: []
    }
  },

created(){
  axios.get(`https://api.punkapi.com/v2/beers?page=2&per_page=80`)
  .then(response => {
    this.beers = response.data
  })
  .catch(e =>{
    this.errors.push(e)
  })
}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
body{
  background: #f2f2f2;
   
}
input{
  border-radius: 3rem;
}
.btn.btn-outline-success{
  border-radius: 3rem;
  transition: all 0.5s;
}
.jumbotron{
 background-image:  linear-gradient(to right, #4DBA87, #2F9088);
background-repeat: no-repeat;
background-size: cover;
height:15rem;
border-radius: 0;
 
}
.jumbotron h1{
  text-transform: uppercase;
  color: #fff;
  padding-top: 3rem;
   font-family: 'Nunito', sans-serif !important;
}
.beers-image img{
  width:10rem;
  height:auto;
}
.card{
  padding: 2rem;
}
@media(max-width:45rem){
 .beers-image img{
  width:5rem;
  height:auto;
} 
}
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.sidebar{
  margin-top: 3rem;
  margin-bottom: 3rem;
}
.sidebar img{
  width:3rem;
  height:auto;
}
</style>
