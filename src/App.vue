<!-- Vue 9: Reactivity -->
<template>
  <div class="card">
    <h2>Message: {{ message }}</h2>
    <h2>Number: {{ number }}</h2>
    <button @click="changeMessageToUpperCase">
      Change Message to Uppercase
    </button>
    <button @click="incrementNumber">Increment Number</button>
  </div>

  <div class="card">
    <h2>Name: {{ wizard.name }}</h2>
    <h2>Wand: {{ wizard.wand }}</h2>
    <button @click="changeNameToUpperCase">Change Name to Uppercase</button>
    <button @click="changeWandCore">Change Wand Core</button>
    <button @click="changeWizard">Change Wizard</button>
  </div>

  <div class="card">
    <h2>Array: {{ wizards }}</h2>
    <button @click="wizards.push('Draco')">Add a New Wizard</button>
  </div>
</template>

<script setup>
import { ref } from 'vue'

let wizards = ref(['Harry', 'Hermione', 'Ron'])

let message = ref('Hello, Reactivity!')
function changeMessageToUpperCase() {
  message.value = message.value.toUpperCase()
  console.log(message.value)
}

let number = ref(1)
function incrementNumber() {
  number.value++
  console.log(number.value)
}

let wizard = ref({
  id: 1001,
  name: 'Harry Potter',
  house: 'Gryffindor',
  age: 17,
  wand: {
    core: 'Phoenix Feather',
    wood: 'Holly'
  }
})

function changeNameToUpperCase() {
  wizard.value.name = wizard.value.name.toUpperCase()
}

function changeWandCore() {
  wizard.value.wand.core = 'Unicorn Hair'
}

function changeWizard() {
  wizard.value = {
    id: 1002,
    name: 'Hermione Granger',
    house: 'Gryffindor',
    age: 17,
    wand: {
      core: 'Dragon Heartstring',
      wood: 'Vine'
    }
  }
}
</script>

<style scoped>
.card {
  background-color: purple;
  color: white;
  padding: 20px 10px;
  margin-bottom: 10px;
}
</style>

<!--  Vue 8: V-bind -->
<!-- <template>
  <h1>{{ message }}</h1>
  <img v-bind:src="imageUrl" alt="">
  <br>
  <img :src="imageUrl" alt="">
  <br>
  <button @click="changeImg">Change image</button>
  <br>

  <hr>
  <input type="text" :value="defaultInputText">
  <hr>

  <p :class="className">Harry Potter</p>
  <p :class="{ inactive: isInactive, center: isCenter }">
    Harry Potter
  </p>
  <p :class="['active', 'center']">Harry Potter</p>
</template>

<script setup>
import { ref } from 'vue'

let message = 'Hello, v-bind!'
let imageUrl = ref('public/img/banner_1.jpg')

function changeImg() {
  imageUrl.value = 'public/img/banner_2.jpg'
}

let defaultInputText = 'Write something here...'
let className = 'active'
let isInactive = ref(true)
let isCenter = ref(false)
</script>

<style scoped>
img {
  max-width: 300px;
}

.active {
  color: green;
}

.inactive {
  color: red;
  text-decoration: line-through;
}

.center {
  text-align: center;
}
</style> -->

<!-- Vue 7: Mustache Notation -->
<!-- <template>
  <h1>message: {{ message }}</h1>
  <hr>
  <h1>number: {{ number }}</h1>
  <hr>
  <h1>doubleNum(50): {{ doubleNum(50) }}</h1>
  <hr>
  <h1>number * 2 = {{ number * 2 }}</h1>
  <hr>
  <h1>{{
    number > 150 ? "number is greater than 150" : "number is less than 150"
  }}</h1>
  <hr>
  <h1 v-text="number"></h1>
  <hr>
  <h1>{{  harry }}</h1>
  <h1>{{ harry.name }}</h1>
  <hr>
  <h1>{{ hogwartsWizards }}</h1>
  <h1>{{ hogwartsWizards[0] }}</h1>
  <hr>
  <h1>{{  rawHtml }}</h1>
  <h1 v-text="rawHtml"></h1>
  <h1 v-html="rawHtml"></h1>
</template>

<script setup>
let message = "Hello, Vue!"
let number = 50;

function doubleNum(num) {
  return num * 2
}

let harry = {
  id: 1001,
  name: 'Harry Potter',
  house: 'Gryffindor',
  age: 17, // Age during the final battle of Hogwarts
  wand: {
    core: 'Phoenix feather',
    wood: 'Holly'
  }
}

const hogwartsWizards = [
  {
    id: 1001,
    name: 'Harry Potter',
    house: 'Gryffindor',
    age: 17,
    wand: {
      core: 'Phoenix feather',
      wood: 'Holly'
    }
  },
  {
    id: 1002,
    name: 'Hermione Granger',
    house: 'Gryffindor',
    age: 17,
    wand: {
      core: 'Dragon heartstring',
      wood: 'Vine'
    }
  },
  {
    id: 1003,
    name: 'Ron Weasley',
    house: 'Gryffindor',
    age: 17,
    wand: {
      core: 'Unicorn hair',
      wood: 'Willow'
    }
  },
  {
    id: 1004,
    name: 'Draco Malfoy',
    house: 'Slytherin',
    age: 17,
    wand: {
      core: 'Dragon heartstring',
      wood: 'Hawthorn'
    }
  }
]

let rawHtml = '<span style="color: red">This should be red.</span>'
</script>

<style lang="scss" scoped></style> -->