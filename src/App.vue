<script setup>
import { ref, computed } from 'vue';

const name = 'dynamic Vue JS'
const styleColor = "color: blue";

const arrColor = ["Blue", "Yellow", "Green", "Peru"];

const active = false;
const arrIconFruits = ["🍎", "🍌", "🍉", "🍓", "🍒"];

const arrFruits = [
  {
    name: "Manzana",
    price: "$1.00",
    description: "Una manzana",
    stock: 0,
    id: 1
  },
  {
    name: "Pera",
    price: "$2.00",
    description: "Una pera",
    stock: 10,
    id: 2
  },
  {
    name: "Naranja",
    price: "$3.00",
    description: "Una naranja",
    stock: 20,
    id: 3
  },
];

const objFruit = {
  name: "Manzana",
  price: "$1.00",
  description: "Una manzana",
  id: 1
};

const users = [
  {
    id: 1,
    name: 'Juan',
    posts: [
      { id: 1, title: 'Mi primer post' },
      { id: 2, title: 'Mi segundo post' },
    ]
  },
  {
    id: 2,
    name: 'Maria',
    posts: [
      { id: 3, title: 'Mi tercer post' },
      { id: 4, title: 'Mi cuarto post' },
    ]
  }
];

const handleClick = (msg) => {
  console.log(msg);
}

const counter = ref(0);
const increaseCounter = () => counter.value++
const decreaseCounter = () => counter.value --
const resetCounter = () => ( counter.value = 0 );

const styleCounter = computed(() => {
  let defaultValue = 'zero';

  if(counter.value > 0) {
    defaultValue = 'positive';
  }

  if(counter.value < 0) {
    defaultValue = 'negative';
  }

  return defaultValue;
})

let favoriteNumber = ref([]);

const addToFavorite = () => {
  favoriteNumber.value.push(counter.value);
}

const blockBtnAdd = computed(() => {
  const result = favoriteNumber.value.find((item) => item === counter.value);
  return result || result === 0;
})
</script>

<template>  
  <!-- Reactive counter based on v-on -->
  <h1>Hello {{ name.toUpperCase() }} !</h1>
  <h2 :class="styleCounter">{{ counter }}</h2>
  <ul>------------------- BASIC CLICK -------------------</ul>
  <div class="container">
    <button v-on:click="increaseCounter" class="btn btn-success">Increase</button>
    <button v-on:click="decreaseCounter" class="btn btn-danger">Decrease</button>
    <button v-on:click="resetCounter" class="btn btn-secondary">Reset</button>
    <button @click="addToFavorite" :disabled="blockBtnAdd" class="btn btn-primary">Add</button>

    <ul class="list-group">
      <li
      class="list-group-item"
      v-for="(favorite, index) in favoriteNumber" :key="index">
        {{ favorite }}
      </li>
    </ul>
</div>
</template>

<!-- <template>  //Directive v-on
  <h1>Hello {{ name.toUpperCase() }} !</h1>
  <ul>------------------- BASIC CLICK -------------------</ul>
  <button v-on:click="handleClick('Activated 1')">Activate 1</button>
  <button @click="handleClick('Activated 2')">Activate 2</button>

  <ul>------------------- All CLICK -------------------</ul>
  <button v-on:click.right.prevent="handleClick('Right')">Right Click</button>
  <button @click.middle="handleClick('Middle')">Middle Click</button>
  <button @click="handleClick('Left')">Left Click</button>
</template> -->

<!-- <template>  //Javascritp expressions
  <h1>Hello {{name.toUpperCase()}} !</h1>
  <h2 :style="styleColor"> Blue line</h2>
  <h2>{{ arrColor }}</h2>
  <h2 :style="`color: ${arrColor[3]}`">{{ arrColor[3] }}</h2>

  <h2>
    {{ active ? 'I am active' : 'I am not active' }}
  </h2>
</template> -->

<!-- <template>  //Directives v-if  v-else-if  v-else
  <h1>Hello {{name.toUpperCase()}} !</h1>

  <h2 v-if="active === true">
    <span>Icon</span>
    I am active
  </h2>

  <p v-if="!active">I am not active</p>
  <p v-else-if="active === false">I am not active</p>
  <p v-else>I don't know</p>

  <h2 v-show="active">I am active from v-show</h2>
</template>  -->

<!-- <template>  //Directive v-for
  <h1>Hello {{name.toUpperCase()}} !</h1>

  <ul>------------------- ITERATE AN ICON ARRAY -------------------</ul>
  <h2>{{ arrIconFruits }}</h2>
  <ul>
    <li
      v-for="(fruit, index) in arrIconFruits"
      :key="index"
    >
      {{index}} - {{ fruit }}
    </li>
  </ul>

  <ul>------------------- ITERATE AN ARRAY -------------------</ul>
  <ul>
    <li v-for="fruit in arrFruits" :key="arrFruits.id">
      {{ fruit.name }} - {{ fruit.price }} - {{ fruit.description }}
    </li>
  </ul>

  <ul>------------------- ITERATE AN OBJECT -------------------</ul>
  <ul>
    <li v-for="(value, key, index) of objFruit" :key="index">
      {{ index }} - {{ key }} : {{ value }}
    </li>
  </ul>
</template> -->

<!-- <template>  //Directives v-for  &&  v-if
  <h1>Hello {{name.toUpperCase()}} !</h1>

  <template  v-for="fruit in arrFruits" :key="fruit.id">
      <ul>
        <li v-if="fruit.stock > 0">
          {{ fruit.name }} - {{ fruit.price }}
        </li>
      </ul>
  </template>
</template> -->

<!-- <template>  //Directive v-for recursive
<h1>Hello {{name.toUpperCase()}} !</h1>

  <div>
    <h2>User list:</h2>
    <ul>
      <template v-for="item in users" :key="item.id">
        <li>
          <h3>
            {{ item.name }}
            <ul>
              <template v-for="post in item.posts" key="post.id">
                <li>
                  <h4>
                    {{ post.title }}
                  </h4>
                </li>
              </template>
            </ul>
          </h3>
        </li>
      </template>
    </ul>
  </div>
</template> -->

<style>
  h1 {
    color: black;
    font-size: 14;
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    font-weight: bold;
  }

  h2 {
    font-size: 12;
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    font-weight: bold;
  }

  .positive {
    color: green;
  }
  .negative {
    color: red;
  }
  .zero {
    color: peru;
  }
</style>
