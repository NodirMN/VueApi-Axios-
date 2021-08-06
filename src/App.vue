<template>
  <div id="app">
    <h1>Persons</h1>
    <div class="per">
    <input type="text" placeholder="Name" v-model="person.name">
    <input type="number" placeholder="age" v-model="person.age">
    <select v-model="person.depart">
        <option value="Veb ilova">Veb ilova</option>
        <option value="Mobil ilova">Mobil ilova</option>
        <option value="Menijment">Menijment</option>
    </select>
    <button class="add" @click="add()">Add</button>
    </div>
    <hr>
    <table width="100%" cellspacing="0" border="1">
      <tr>
        <th>№</th>
        <th>Name</th>
        <th>Age</th>
        <th>Depart</th>
        <th>Delet button</th>
      </tr>
      <tr v-for ='(person,index) of persons' :key='index'>
          <td>{{person.id}}</td>
          <td>{{person.name}}</td>
          <td>{{person.age}}</td>
          <td>{{person.depart}}</td>
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
        persons:[],
        person:{}
      }
    },
    methods: {
      add(){
        axios.post('http://localhost:3000/persons',this.person).then(response => {this.persons.push(response.data)
        this.person = {}
        })
    },
    del(index){
      console.log(this.persons[index])
      axios.delete('http://localhost:3000/persons/'+this.persons[index].id).then(response => {console.log(response.data) 
      this.persons.splice(index,1)
      })
    }
    },
    created(){
      axios.get('http://localhost:3000/persons').then(response => {this.persons = response.data})
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
