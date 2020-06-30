<template>
  <div class="hello">
    <h1>Connect with fruits near you.</h1>
    <h3>Search</h3>
    <div id="options">
      <div class="option">
        <label for="name">Name</label>
        <input type="text" id="name" v-model="nameInput">
      </div>

      <div class="option">
        <label for="color">Color</label>
        <select name="color" id="color" v-model="colorInput">
          <option value=""></option>
          <option value="yellow">Yellow</option>
          <option value="red">Red</option>
          <option value="brown/white">Brown/white</option>
          <option value="orange">Orange</option>
          <option value="purple">Purple</option>
          <option value="green">Green</option>
        </select>
      </div>

      <div class="option">
        <label for="seeds">seeds</label>
        <select name="seeds" id="seeds" v-model="seedsInput">
          <option value=""></option>
          <option value="true">True</option>
          <option value="false">False</option>
        </select>
      </div>
    </div>
    <button v-on:click="filterResults">Search</button> 

    <h3>Results:</h3>
    <ul>
      <li id="resultLabels">
        <p>No.</p>
        <p>Name</p>
        <p>Color</p>
        <p>Seeds</p>
      </li>
      <li v-for="(fruit,index) in this.displayedFruits" :key='index'>
        <p>{{index + 1}}</p>
        <p>{{fruit.name}}</p>
        <p>{{fruit.color}}</p>
        <p>{{fruit.seeds}}</p>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Fruits',
  props: {
    colorFilter: String
  },
  data(){
    return {
      fruits:null,
      displayedFruits:[],
      nameInput:null,
      colorInput:'',
      seedsInput:null,
      queryUrl:null
    }
  },
  methods:{
    filterResults(){
      this.displayedFruits = [];

      //color input
      if(this.colorInput != ''){
        for(var a = 0; a < this.fruits.length; a++){
          //color
          if(this.fruits[a].color == this.colorInput){
            this.displayedFruits.push(this.fruits[a]);
          }
        }
      } else {
        for(var b = 0; b < this.fruits.length; b++){
          this.displayedFruits.push(this.fruits[b]);
        }
      }

      //seeds input
      var seedCheckArr=[];
      //seeds: false
      if(this.seedsInput == 'false'){
        for(var c = 0; c < this.displayedFruits.length; c++){
          if(this.displayedFruits[c].seeds == false){
            seedCheckArr.push(this.displayedFruits[c])
          }
        }
        this.displayedFruits = seedCheckArr;
        console.log(this.displayedFruits)

        //seeds: true
      } else if(this.seedsInput == 'true'){
        for(var d = 0; d < this.displayedFruits.length; d++){
          if(this.displayedFruits[d].seeds == true){
            seedCheckArr.push(this.displayedFruits[d])
          }
        }
        this.displayedFruits = seedCheckArr;
        console.log(this.displayedFruits)
      }
      // -------------------------------------------------------------------
      // var nameCheckArr = [];
      // this.displayedFruits.forEach(fruit=>{
      //   for(var e = 0; e < this.nameInput.length; e++){
      //     if(fruit.name.indexOf(this.nameInput[e] == [e])){
      //       console.log('Fruit ' + fruit.name + ' has letter ' + this.nameInput[e] + ' in the ' + e + ' index.')
      //       }
      //       console.log(this.nameInput[e])
      //     }
      // })
      // -------------------------------------------------------------------
    }
  },
  mounted(){
    // console.log(this.fruitlist)
    axios.get('https://api.npoint.io/f269a79054732da09eb2')
    .then(response=>{
      //da su sva voca kod nas u bazi podataka
      this.fruits = response.data.allFruits;

      this.displayedFruits = this.fruits;
      console.log(this.displayedFruits)
    })
    .catch(()=>{
      alert('No results for you.')
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
  width: 60%;
  margin: 0 auto;
}
li {
  margin: 0 10px;
  display: flex;
  justify-content: space-between;
  text-align: left;
  border-bottom: 1px solid #333;
}

#resultLabels p {
  font-weight: bold;
}

li p {
  width:100px;
  margin:15px 0 5px 0;
}
a {
  color: #42b983;
}

#options {
  /* border:1px solid red; */
  display: flex;
  justify-content: center;
}

.option {
  display: flex;
  flex-direction: column;
  padding:0 30px;
  text-align: center;
}

.option input {
  margin:0 auto;
}
</style>
