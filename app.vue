<script setup lang="ts">
 import {Gender,Popularity,Length,names} from "@/data"

interface optionsState {
  gender: string;
  popularity:string;
  length: string;
}

const computeSelectedNames = () =>{
  const filteredNames = names
      .filter((name) => name.gender === options.gender)
      .filter((name) => name.popularity === options.popularity)
      .filter((name) => {
        if(options.length === Length.ALL) return true
        else return name.length === options.length
      })

      selectedNames.value = filteredNames.map((name) => name.name);
};

const selectedNames = ref<string[]>([]);

const removeName = (index : number) =>{
  const filterName = [...selectedNames.value]
  filterName.splice(index,1)
  selectedNames.value = filterName
}
const optionsArray = [
  {
    title: "1) Choose a gender",
    category: "gender",
    buttons:[Gender.GIRL,Gender.UNISEX,Gender.BOY]
  },
  {
    title: "2) Choose The name's popularity",
    category: "popularity",
    buttons:[Popularity.TRENDY,Popularity.UNIQUE]
  },
  {
    title: "3) Choose name's lenght",
    category: "length",
    buttons:[Length.SHORT,Length.ALL,Length.LONG]
  },
];


  const options = reactive<optionsState>({
  gender:Gender.BOY,
  length:Length.ALL,
  popularity:Popularity.TRENDY,
  });
  
</script>
<template>
  <div class="container">
    <h1>Baby Name Generator</h1>
    <p>Please Choose the Option below to generate name</p>
    <div class="options-container">
     <Option v-for="option in optionsArray" 
     :key="option.title" 
     :option="option" 
     :options = "options"
     />
      
      <button class="primary" @click="computeSelectedNames">Find</button>
    </div>
     <div class="cars-container">
       <CardName 
       v-for="(name,index) in selectedNames" 
       :key="name" 
       :name ="name" 
       @remove = "() =>removeName(index)" 
       :index ="index" 
       />
       
    </div>
  </div>
</template>



<style scoped>
.container{
  font-family: Arial, Helvetica, sans-serif;
  color: rgb(27, 60, 138);
  max-width: 50rem;
  margin: 0 auto;
  text-align: center;
}

.h1{
  font-size: 3rem;
}

.options-container{
  background-color: rgb(255, 238, 236);
  border-radius: 2rem;
  padding: 1rem;
  width: 95%;
  margin: 0 auto;
  margin-top: 4rem;
  position: relative;
}


.primary{
  background-color: rgb(249, 87, 89);
  color: white;
  border-radius: 6.5rem;
  padding: 0.75rem;
  width: 12rem;
  outline: 0.15rem solid rgb(249, 87, 89);
  cursor:pointer;
  border: none;
  font-size: 1.2rem;
}
.cars-container{
  display: flex;
  margin-top: 3rem;
  flex-wrap: wrap;
}

</style>
