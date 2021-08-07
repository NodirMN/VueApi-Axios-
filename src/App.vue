<template>
  <div id="app">
    <h1>Cars</h1>
    <div class="per">
    <input type="text" placeholder="Name" v-model="car.model">
    <select v-model="car.color">
        <option value="Qora">Qora</option>
        <option value="Oq">Oq</option>
    </select>
    <input type="number" placeholder="Year" v-model="car.year">
    <input type="number" placeholder="Distance" v-model="car.distance">
    <select v-model="car.depart">
        <option value="Xechbek">Xechbek</option>
        <option value="Sedan">Sedan</option>
        <option value="Kupe">Kupe</option>
    </select>
    <button class="add" @click="add()">Add</button>
    </div>
    <hr>
    <table width="100%" cellspacing="0" border="1">
      <tr>
        <th>№</th>
        <th>Model</th>
        <th>Color</th>
        <th>Year of manufacturet</th>
        <th>Pressing distance</th>
        <th>Cars body</th>
        <th>Delet button</th>
      </tr>
      <tr v-for ='(car,index) of cars' :key='index'>
          <td>{{car.id}}</td>
          <td>{{car.model}}</td>
          <td>{{car.color}}</td>
          <td>{{car.year}}</td>
          <td>{{car.distance}}</td>
          <td>{{car.depart}}</td>
          <td>
            <button class="dell" @click="del(index)">Delet</button>
          </td>
      </tr>
    </table>

  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'App',
    data(){
      return{
        cars:[],
        car:{}
      }
    },
    methods: {
      add(){
        axios.post('http://localhost:3000/cars',this.car).then(response => {this.cars.push(response.data)
        this.car = {}
        })
    },
    del(index){
      console.log(this.cars[index])
      axios.delete('http://localhost:3000/cars/'+this.cars[index].id).then(response => {console.log(response.data) 
      this.cars.splice(index,1)
      })
    }
    },
    created(){
      axios.get('http://localhost:3000/cars').then(response => {this.cars = response.data})
    }
}
</script>

<style>
.add{
  background-color: rgb(172, 206, 21);
  border: 0;
  cursor: pointer;
  padding: 10px;
  border-radius: 10px;
}
.dell{
  background-color: rgb(206, 21, 21);
  border: 0;
  cursor: pointer;
  padding: 10px;
  border-radius: 10px;
}
.per{
    display: flex;
    justify-content: space-around;
}
</style>
