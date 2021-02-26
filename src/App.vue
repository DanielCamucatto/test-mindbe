<template>
  <div id="app">
    <header>
          <nav>
            <figure class="image is-128x128">
              <img src="./assets/img/logo.png" alt="">
            </figure>
              
              <ul>
                  <li class="button is-dark is-small">Home</li>
                  <li class="button is-dark is-small">Sobre</li>
                  <li class="button is-dark is-small">Contato</li>
              </ul>
          </nav>
      </header>
      <main>
        <h1>Contact<span> Studio</span></h1>
          <div class="btn"><p>buscar posts de usuário</p>
          <div class="select" >
            <select id="userId" v-model="selected" required >
              <option selected>Selecione um usuário</option>
              <option  type='selected' v-for=" id in ids" v-bind:key="id.id">{{id.id}}</option> 
            </select>
          </div>
          <button id="btn-search" class="button is-dark is-small" type="submit" @click="searchId">procurar</button>
        </div>
        <section id="card-container">
          <div class="card-box" v-for="user in users" v-bind:key="user.post">
            <div class="card" >
            <div class="card-header" >
              <p>{{user.title}}</p>
            </div>
            <div class="card-content">
            {{user.body}}
            </div>
          </div>
          
          </div>
          
        </section>
      </main>
      <footer>
        <div class="contact">
            <div class="fone"> Contato: (11) 99999-999</div>
            <div class="email">E-mail:contact@studio.com.br</div>
        </div>
        <div class="studio-branding">
            <p>Contact Studio&reg;</p>
        </div>
          
      </footer>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'App',
  data(){
    return{
      selected: [],
      ids:[],
      users:[{}]
    }
  },
  created(){
    axios.get('https://jsonplaceholder.typicode.com/posts').then(resp => {
      //this.users = resp.data;
      this.ids = resp.data
    })
  },
  methods:{
    searchId(){
        const selected = document.getElementById('userId').value;
          console.log(selected);
          
      axios.get('https://jsonplaceholder.typicode.com/posts').then(resp => {
      //this.users = resp.data;
      this.users = resp.data
      for( let user of this.users){
        console.log(user.userId)
          if(user.id == selected){
            //this.users = user.userId
            user.userId = this.users;
          }
      }
    })
      
              
    }  
  }
} 
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Nunito:ital,wght@0,200;0,300;0,400;0,600;0,700;0,800;0,900;1,200;1,300;1,400;1,600;1,700;1,800;1,900&display=swap");
@import "https://cdn.jsdelivr.net/npm/bulma@0.9.1/css/bulma-rtl.min.css";
html, body{
    margin: 0px; 
    padding: 0px;
    box-sizing: border-box;
    font-family:  'nunito', sans-serif;
    width: 100%;
    height: 100%;
}
#app{
  display: grid;
  grid-template-rows: auto auto auto;
  grid-template-columns: 1fr 1fr;
  grid-template-areas: 
  "header header"
  "main main"
  "footer footer"
  ;
  
}
header{
  background-color:white;
  grid-area: header;
  height: 100%;
}
figure{
  margin: auto;
}
nav{
  display: grid;
  padding: 10px;
}
nav h3{
  grid-column-start: 1;
  margin: auto;
}
nav ul{
  display: flex;
  grid-column-start: 2;
  justify-content: space-evenly;
  list-style: none;
  align-items: center;
  text-align: center;
  text-transform: uppercase;
  width: 60%;
  margin: auto;
}
main{
  grid-area: main;
  height: 100%;
}
main h1{
  border: solid 1px white;
  display: block;
  margin: 5% auto;
  text-align: center;
  font-size: 2rem;
  font-weight: bolder;
  text-transform: uppercase;
}
h1 span{
  font-weight: 400;
}
.btn{
  display: block;
  margin: 5% auto;
  text-align: center;
}
.btn p{
  font-size: 1.2rem;
  font-style: italic;
  font-weight: 500;
  padding: 2%;
}
.input{
  width: 30%;
  border-radius: 5px 0px 0px 5px;
}
#btn-search{
  padding: 1.6em;
  border-radius: 0px 5px 5px 0px;
}
#card-container{
  border: solid 1px white;
  display: grid;
  grid-template-columns: repeat(4,auto);
  grid-gap: 50px;
  margin: 5% auto;
  width: 70%;
  padding: 3%;
  box-shadow: -5px 0px 52px 0px rgba(0,0,0,0.42);
  -webkit-box-shadow: -5px 0px 52px 0px rgba(0,0,0,0.42);
  -moz-box-shadow: -5px 0px 52px 0px rgba(0,0,0,0.42);
}
.card-box{
  width: 100%;
  margin: auto;
}
.card{
  padding: auto;
  border: solid 1px white;
  box-shadow: -5px 0px 52px 0px rgba(0,0,0,0.42);
  -webkit-box-shadow: -5px 0px 52px 0px rgba(0,0,0,0.42);
  -moz-box-shadow: -5px 0px 52px 0px rgba(0,0,0,0.42);
}
.card-header{
  padding: 3%;
  font-weight: bold;
  font-style: italic;
}
.card-content{
  text-align: justify;
}
footer{
  background-color: grey;
  display: grid;
  justify-content:space-around;
  align-items: center;
  grid-area: footer;
  margin-bottom: 2%;
  height: 100%;
}
.fone{
  grid-column-start: 1;
  justify-content: center;
  color: aliceblue;

}
.email{
  grid-column-start: 1;
  color: aliceblue;
}
.studio-branding{
  display: grid;
  grid-column-start: 2;
  text-align: center;
  align-content: center;
  color: aliceblue;
}
</style>
