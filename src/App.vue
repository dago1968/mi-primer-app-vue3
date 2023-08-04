<script setup>
  import { ref, computed } from 'vue';
/**
 * ref()
    ref es una forma de trabajar con la reactividad de Vue 3.
   ºref: Es una referencia reactiva, en nuestro ejemplo necesitamos 
   un entero que sea "rastreable", por ende utilizaremos ref, una forma 
   de trabajar con la reactividad de Vue 3.
   ref toma el argumento y lo devuelve envuelto dentro de un objeto 
   con una value propiedad, que luego puede usarse para acceder o 
   mutar el valor de la variable reactiva.
   DOM: Cuando muta el estado reactivo, el DOM se actualiza 
   automaticamente.
   En el template no es necesario acceder al .value, ya que el 
   valor de la variable reactiva se puede acceder directamente.
 */
/**
 * computed, son para realizar las propiedades computadas; esta computed
 * recibe una funcion de flecha; esta funcion siempre debe retormar 
 * algo
 */
  const titulo = "Con reactividad";
  const styleColor = "color: blue";

  // metodo - methods
  const handleClick = (message) => {
    console.log(message)
  }

  const counter = ref(0);
  const stateCounter = ["red", "green"];

  const increment = () => {
    counter.value++;
  };

  const decrement = () => {
    counter.value--;
  };

  const reset = () => {
    counter.value = 0;
  } 

  const arrayNumber = ref([]);

  const addArray = () => {
    arrayNumber.value.push(counter.value);
  }

  const bloquearBtnAdd = computed(() => {
    const numSearch = arrayNumber.value.find((num) => num === counter.value)
    //console.log(numSearch);
    if(numSearch === 0) return true;
    return numSearch ? true : false;
    //return numSearch || numSearch === 0;
  })

  const classCounter = computed(() => {
    if(counter.value === 0) {
      return 'zero'
    }
    if(counter.value > 0) {
      return 'positive'
    }
    if(counter.value < 0) {
      return 'negative'
    }
  })
</script>

<template>
  <div class="container text-center mt-3">

      <h1>Curso VueJs {{ titulo.toUpperCase() }}</h1>
      <h3 :style="styleColor">Por: Dagoberto Hernández García</h3>
      <hr>
      
      <!-- Contador -->
      <h2>Contador</h2>
      <div class="btn-group">
        <button @click="increment()" class="btn btn-success">+</button>
        <button @click="decrement()" class="btn btn-danger">-</button>
        <button @click="reset()" class="btn btn-secondary">Resetear</button>
        <button @click="addArray()" :disabled="bloquearBtnAdd" class="btn btn-primary">add</button>
      </div>
      
    
      <!-- Otra forma de hacerlo es con clases reactivas, como se ve a continuación-->
      <h2>Contador: <span :class="classCounter">{{ counter }}</span></h2>
      <h2 :class="classCounter"> Contador: {{ counter }} </h2>
    
      <h2>Números escogidos</h2>
      
      <ul class="list-group">
        <li class="list-group-item mt-4"
          v-for="(numero, index) in arrayNumber" :key="index"
          > {{ index + 1 }} - {{ numero }}
        </li>
      </ul>
  </div>

</template>

<style scoped>

.positive {
  color: green;
}

.negative {
  color: red
}

.zero {
  color: peru;
}

li {
  list-style: none;
}
  

</style>
