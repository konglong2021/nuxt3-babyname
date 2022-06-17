<script setup lang="ts">
interface NameProps{
  name: string;
  index: number
}

const props = defineProps<NameProps>();
const emit = defineEmits(["remove"]);
const removeName = () =>{
  emit("remove", props.index);
};
</script>

<template>
     <div class="card" >
        <h4>{{name}}</h4>
        <p @click="removeName">x</p>
     </div>
</template>

<style scoped>
.card{
  background-color: rgb(27, 60, 138);
  color: white;
  width: 28%;
  padding: 0.1rem;
  margin-right: 0.5rem;
  margin-bottom: 1rem;
  border-radius:1rem;
  border: none;
  position: relative;
 box-shadow:
  0 2.8px 2.2px rgba(0, 0, 0, 0.034),
  0 6.7px 5.3px rgba(0, 0, 0, 0.048),
  0 12.5px 10px rgba(0, 0, 0, 0.06),
  0 22.3px 17.9px rgba(0, 0, 0, 0.072),
  0 41.8px 33.4px rgba(0, 0, 0, 0.086),
  0 100px 80px rgba(0, 0, 0, 0.12)
;
}

.card p{
  position: absolute;
  top: -30%;
  left: 93.5%;
  cursor: pointer;
  color: rgb(255, 255, 255,0.178);
}
</style>