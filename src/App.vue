<!-- Vue 10: V-on -->

<template>
  <h1>{{ message }}</h1>
  <button v-on:click="replaceText('V-on is fun!')">
    Replace Text
  </button>
  <button @click="replaceText('V-on is fun!')">
    Replace Text
  </button>

  <hr>

  <p>
    An input field where the user can ONLY enter numbers:
  </p>
  <input type="text" @keydown="handleInput($event)">

  <hr>

  <p>
    A demo of preventing the default behavior of an event.
  </p>
  <p>
    Right click in the cyan box below will not show the context menu:
  </p>
  <div
    style="width: 100px; height: 100px; background-color: aqua"
    @contextmenu.prevent="console.log('Show a custom context menu instead.')"
  ></div>

  <hr>

  <p>
    A demo of stopping event propagation:
  </p>
  <div id="mouseover" @mouseover="fun1">
    <textarea @mouseover.stop="fun2($event)">
      This is a text area.
    </textarea>
  </div>

  <hr>

  <div>
    Press down the "Enter" key will trigger a console log print:
    <input
      type="text"
      @keydown.enter="console.log('You pressed the Enter key.')"
    />
  </div>
  <div>
    Press down the "Arrow Down" key will trigger a console log print:
    <input
      type="text"
      @keydown.down="console.log('You pressed the Arrow Down key.')"
    />
  </div>
  <div>
    Press down the "Space" key will trigger a console log print:
    <input
      type="text"
      @keydown.space="console.log('You pressed the Space key.')"
    />
  </div>
  <div>
    Press down the "b" key will trigger a console log print:
    <input 
      type="text" 
      @keydown.b="console.log('You pressed the B key.')" 
    />
  </div>
  <div>
    Press down the "Ctrl+C" will trigger a console log print:
    <input 
      type="text" 
      @keydown.ctrl.c="console.log('You pressed Ctrl+C.')" 
    />
  </div>
</template>

<script setup>
import { ref } from 'vue'

let message = ref('Hello, V-on!')
function replaceText(msg) {
  message.value = msg
}

function handleInput(event) {
  let keyCode = event.keyCode
  if (keyCode < 48 || keyCode > 57) {
    event.preventDefault()
  }
}

function fun1() {
  console.log('Mouse Over Div')
}

function fun2(event) {
  console.log('Mouse Over TextArea')
}
</script>

<style scoped>
#mouseover {
  text-align: right;
  background-color: purple;
  width: 300px;
  height: 300px;
}
</style>

<!-- Vue 9: Reactivity -->
<!-- <template>
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
</style> -->

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