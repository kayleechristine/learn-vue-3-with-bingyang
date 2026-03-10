<!-- Vue 18: watchEffect -->
 <template>
  <h1>{{ message }}</h1>

  <div>
    <form @submit.prevent="register">
      <div>
        <label for="email">Email:</label>
        <input
          id="email"
          v-model="email"
          type="email"
          placeholder="Enter Your Email"
        />
      </div>
      <div>
        <label for="password">Password:</label>
        <input
          id="password"
          v-model="password"
          type="password"
          placeholder="Create a Password"
        />
      </div>
      <button type="submit" :disabled="!isFormValid">Register</button>
    </form>
  </div>

  <hr>

  <div class="card">
    <h2>Name: {{ wizard1.name }}</h2>
    <h2>Wand: {{ wizard1.wand }}</h2>
    <h2>Age: {{ wizard1.age }}</h2>
    <button @click="wizard1.name = wizard1.name.toUpperCase()">
      Change Name to Uppercase
    </button>
    <button @click="wizard1.wand.core = 'Unicorn Hair'">
      Change Wand Core
    </button>
    <button @click="wizard1.age = 20">Change Age</button>
  </div>
</template>

<script setup>
import { ref, watchEffect } from 'vue'

let message = ref('Hello, watchEffect!')
const email = ref('')
const password = ref('')
const isFormValid = ref(false)

watchEffect(() => {
  console.log('watchEffect')
  const hasEmail = email.value.length > 0
  const hasPassword = password.value.length > 0
  isFormValid.value = hasEmail && hasPassword
})

const register = () => {
  alert('Registration successful!')
  // TODO: Registration functionality
}

let wizard1 = ref({
  id: 1001,
  name: 'Harry Potter',
  house: 'Gryffindor',
  age: 17,
  wand: {
    core: 'Phoenix Feather',
    wood: 'Holly'
  }
})

watchEffect(() => {
  console.log(wizard1.value.name, wizard1.value.wand.core)
})

watchEffect(() => {
  console.log(wizard1.value)
})
</script>

<style scoped>
.card {
  background-color: purple;
  color: white;
  padding: 20px 10px;
  margin-bottom: 10px;
}
</style>

<!-- Vue 17: Watchers -->
<!-- <template>
  <h1>{{ message }}</h1>

  <div class="card">
    <h1>Scenario 1: Watch a "ref(primitive value)"</h1>
    <h2>Number: {{ number }}</h2>
    <button @click="number++">Increment Number</button>
  </div>

  <div class="card">
    <h1>Scenario 2: Watch a Property in "ref(object)"</h1>
    <h2>Name: {{ wizard1.name }}</h2>
    <h2>Wand: {{ wizard1.wand }}</h2>
    <button @click="wizard1.name = wizard1.name.toUpperCase()">
      Change Name to Uppercase
    </button>
    <button @click="changeWizard1Wand">Change Wand</button>
    <button @click="wizard1.wand.core = 'Unicorn Hair'">
      Change Wand Core
    </button>
  </div>

  <div class="card">
    <h1>Scenario 3: Watch a "ref(object)"</h1>
    <h2>Name: {{ wizard2.name }}</h2>
    <h2>Wand: {{ wizard2.wand }}</h2>
    <button @click="wizard2.name = wizard2.name.toUpperCase()">
      Change Name to Uppercase
    </button>
    <button @click="wizard2.wand.core = 'Phoenix Feather'">
      Change Wand Core
    </button>
    <button @click="changeWizard">Change Wizard</button>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'

let message = ref('Hello, Watchers!')

let number = ref(1)

// #1: Watch a primitive value
const stopWatch = watch(number, (newValue, oldValue) => {
  console.log(
    'Watch a ref(primitive value): number changes',
    newValue,
    oldValue
  )
  if (newValue >= 5) {
    stopWatch()
  }
})

// #2: Watch a property of an object
let wizard1 = ref({
  id: 1001,
  name: 'Harry Potter',
  house: 'Gryffindor',
  age: 17,
  wand: {
    core: 'Phoenix Feather',
    wood: 'Holly'
  }
})

function changeWizard1Wand() {
  wizard1.value.wand = {
    core: 'Dragon Heartstring',
    wood: 'Vine'
  }
}

watch(
  () => wizard1.value.name,
  (newValue, oldValue) => {
    console.log(
      'Watch a property in a ref(object): wizard1 name changes',
      newValue,
      oldValue
    )
  }
)

watch(
  () => wizard1.value.wand,
  (newValue, oldValue) => {
    console.log(
      'Watch a property in a ref(object): wizard1 wand changes',
      newValue,
      oldValue
    )
  },
  { deep: true }
)

// #3: Watch an object
let wizard2 = ref({
  id: 1003,
  name: 'Ron Weasley',
  house: 'Gryffindor',
  age: 17,
  wand: {
    core: 'Unicorn Hair',
    wood: 'Willow'
  }
})

function changeWizard() {
  wizard2.value = {
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

watch(
  wizard2,
  (newValue, oldValue) => {
    console.log('Watch a ref(object): wizard2 changes', newValue, oldValue)
  },
  { deep: true }
)

// #4: Watch multiple values (primitive array, property of an object, and an object)
watch(
  [number, () => wizard1.value.name, wizard2],
  (newValue, oldValue) => {
    console.log(
      'Watch an array of ref(primitive value), a property of a ref(object), and a ref(object)'
    )
  },
  { deep: true }
)
</script>

<style scoped>
.card {
  background-color: purple;
  color: white;
  padding: 20px 10px;
  margin-bottom: 10px;
}
</style> -->

<!-- Vue 16: Computed Properties -->
<!-- <template>
  <h1>{{ message }}</h1>
  <button @click="sortUsersByAge">Sort Users by Age</button>
  <br>
  <button @click="hideInactive = !hideInactive">{{ toggleButtonName }}</button>

  <h2>Number of Active Users (Computed Property): {{ numberOfActiveUsers }}</h2>
  <h2>Number of Active Users (Computed Property): {{ numberOfActiveUsers }}</h2>
  <h2>Number of Active Users (Computed Property): {{ numberOfActiveUsers }}</h2>

  <h2>Number of Active Users (Method Call): {{ computeNumberOfActiveUsers() }}</h2>
  <h2>Number of Active Users (Method Call): {{ computeNumberOfActiveUsers() }}</h2>
  <h2>Number of Active Users (Method Call): {{ computeNumberOfActiveUsers() }}</h2>

  <table>
    <tr>
      <th>Index</th>
      <th>Id</th>
      <th>Name</th>
      <th>Age</th>
      <th>Operation</th>
    </tr>
    <tr v-for="(user, index) in filteredUsers" :key="user.id">
      <td>{{ index + 1 }}</td>
      <td>{{ user.id }}</td>
      <td :class="{ inactive: !user.isActive }">
        {{ user.name }}
      </td>
      <td>{{ user.age }}</td>
      <td>
        <button @click="user.isActive = !user.isActive">
          {{ user.isActive ? 'Deactivate' : 'Restore' }}
        </button>
      </td>
    </tr>
  </table>
</template>

<script setup>
import { computed, ref } from 'vue'

let message = ref('Hello, Computed Properties!')

const users = ref([
  { id: 1001, name: 'John Smith', age: 26, isActive: false },
  { id: 1002, name: 'Tom Doe', age: 16, isActive: false },
  { id: 1003, name: 'Frankin Wong', age: 18, isActive: true }
])

let hideInactive = ref(false)

function sortUsersByAge() {
  users.value.sort((a, b) => a.age - b.age)
}

let toggleButtonName = computed(() =>
  hideInactive.value ? 'Show all' : 'Hide inactive'
)

let numberOfActiveUsers = computed(() => {
  console.log('computed property')
  return users.value.filter((user) => user.isActive).length
})

let computeNumberOfActiveUsers = () => {
  console.log('method call')
  return users.value.filter((user) => user.isActive).length
}

let filteredUsers = computed(() =>
  hideInactive.value ? users.value.filter((user) => user.isActive) : users.value
)
</script>

<style scoped>
.inactive {
  color: red;
  text-decoration: line-through;
}
</style> -->

<!-- Vue 15: Array Change Detection -->
<!-- <template>
  <h1>{{ message }}</h1>
  <button @click="sortUsersByAge">Sort Users by Age</button>
  <button @click="hideInactiveUsers">Hide Inactive Users</button>
  <button @click="showFirstTwoUsers">Show First Two Users</button>
  <ul>
    <li v-for="(user, index) in users" :key="user.id">
      {{ index }} - {{ user.id }} - {{ user.name }} - {{ user.age }} -
      {{ user.isActive }}
    </li>
  </ul>
</template>

<script setup>
import { ref } from 'vue'

let message = ref('Hello, Array Change Detection!')

const users = ref([
  { id: 1001, name: 'John Smith', age: 26, isActive: false },
  { id: 1002, name: 'Tom Doe', age: 16, isActive: false },
  { id: 1003, name: 'Frankin Wong', age: 18, isActive: true }
])

function sortUsersByAge() {
  users.value.sort((a, b) => a.age - b.age)
}

function hideInactiveUsers() {
  users.value = users.value.filter((user) => user.isActive)
}

function showFirstTwoUsers() {
  users.value = users.value.slice(0, 2)
}
</script>

<style scoped>
.inactive {
  color: red;
  text-decoration: line-through;
}
</style> -->

<!-- Vue 14: V-for -->
<!-- <template>
  <h1>{{ message }}</h1>
  <button @click="sortUsersByAge">
    Sort Users by Age
  </button>
  <ul>
    <li v-for="(user, index) in users" :key="user.id">
      {{ index }} - {{ user.id }} - {{ user.name }} - {{ user.age }} -
      {{ user.isActive }}
    </li>
  </ul>

  <hr>

  <table>
    <tr>
      <th>Index</th>
      <th>Id</th>
      <th>Name</th>
      <th>Age</th>
      <th>Operation</th>
    </tr>
    <tr v-for="(user, index) in users" :key="user.id">
      <td>{{ index }}</td>
      <td>{{ user.id }}</td>
      <td :class="{ inactive: !user.isActive }">{{ user.name }}</td>
      <td>{{ user.age }}</td>
      <td>
        <button @click="user.isActive = !user.isActive">
          {{ user.isActive ? 'Deactivate' : 'Restore' }}
        </button>
      </td>
    </tr>
  </table>

  <hr>

  <p>
    Use v-for to iterate through the properties of an object:
  </p>
  <div v-for="(value, key, index) in users[0]">
    {{ index }} - {{ key }}: {{ value }}
  </div>
</template>

<script setup>
import { ref } from 'vue'

let message = ref('Hello, V-for!')

const users = ref([
  { id: 1001, name: 'John Smith', age: 26, isActive: false },
  { id: 1002, name: 'Tom Doe', age: 16, isActive: false },
  { id: 1003, name: 'Frankin Wong', age: 18, isActive: true }
])

function sortUsersByAge() {
  users.value.sort((a, b) => a.age - b.age)
}
</script>

<style scoped>
.inactive {
  color: red;
  text-decoration: line-through;
}
</style> -->

<!-- Vue 13: V-if -->
<!-- <template>
  <h1>{{ message }}</h1>
  <p>
    What has keys but can't open locks, 
    space but no room, 
    and you can enter but
    can't go outside? What am I?
  </p>

  <button style="width: 200px" @click="showAnswer = !showAnswer">
    {{ !showAnswer ? 'Show me the answer!' : 'Hide the answer!' }}
  </button>

  <div v-if="showAnswer">A keyboard.</div>
</template>

<script setup>
import { ref } from 'vue'

let message = ref('Hello, V-if!')
let showAnswer = ref(false)
</script>

<style scoped></style> -->

<!-- Vue 12: V-Model & V-Bind -->
<!-- <template>
  <h1>V-Model vs V-Bind</h1>
  <h2>message: {{ message }}</h2>
  <div>
    <p>v-model = v-bind + @input</p>
    <input
      type="text"
      v-bind:value="message"
      @input="message = $event.target.value"
    />
  </div>
  <div>
    <p>v-model</p>
    <input 
      type="text" 
      v-model="message" 
    />
  </div>
</template>

<script setup>
import { ref } from 'vue'

let message = ref('Hello!')
</script>

<style scoped></style> -->

<!-- Vue 11: V-Model -->
<!-- <template>
  <h1>{{ message }}</h1>
  <h1>Welcome, {{ formData.name }}</h1>

  <form action="">
    <div>
      <span>Name:</span>
      <span>
        <input 
        type="text" 
        v-model.lazy="formData.name"
      />
      </span>
    </div>

    <div>
      <span>Gender:</span>
      <span>
        <input 
          type="radio" 
          id="male" 
          value="M" 
          v-model="formData.gender" 
        />
        <label for="male">M</label>
        <input 
          type="radio" 
          id="female" 
          value="F" 
          v-model="formData.gender" 
        />
        <label for="female">F</label>
      </span>
    </div>

    <div>
      <span>Age:</span>
      <span>
        <input 
          type="text" 
          id="age" 
          v-model.number="formData.age" 
        />
      </span>
    </div>

    <div>
      <span>Hobbies:</span>
      <input 
        type="checkbox" 
        value="basketball" 
        v-model="formData.hobbies" 
      />
      <label for="basketball">Basketball</label>
      <input 
        type="checkbox" 
        value="football" 
        v-model="formData.hobbies" 
      />
      <label for="football">Football</label>
      <input 
        type="checkbox" 
        value="js" 
        v-model="formData.hobbies" 
      />
      <label for="js">JavaScript</label>
    </div>

    <div>
      <span>Profession:</span>
      <select v-model="formData.profession">
        <option value="">Please select one</option>
        <option value="1">Software Engineer</option>
        <option value="2">Data Scientist</option>
        <option value="3">Product Manager</option>
        <option value="4">Professor</option>
      </select>
    </div>

    <div>
      <span>Description:</span>
      <textarea
        v-model.trim="formData.desc"
        @keyup.enter="submitForm"
      ></textarea>
    </div>

    <div>
      <input 
        type="reset" 
        value="Reset" 
        @click="resetForm" 
      />
      <input 
        type="submit" 
        value="Submit" 
        @click.prevent="submitForm" 
      />
    </div>
  </form>
</template>

<script setup>
import { ref } from 'vue'

let message = ref('Hello, V-model!')

let formData = ref({
  name: '',
  gender: '',
  age: '',
  hobbies: [],
  profession: '',
  desc: ''
})

function resetForm() {
  formData.value = {
    name: '',
    gender: '',
    age: '',
    hobbies: [],
    profession: '',
    desc: ''
  }
}

function submitForm() {
  console.log(JSON.stringify(formData.value))
}
</script>

<style scoped>
form {
  padding: 20px;
}

form div {
  height: 40px;
  line-height: 40px;
}

form div span {
  display: inline-block;
  width: 100px;
}
</style> -->

<!-- Vue 10: V-on -->
<!-- <template>
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
</style> -->

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