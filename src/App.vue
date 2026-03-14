<!-- Vue 29: Scoped Slots -->
<template>
  <StudentList :list="list">
    <template #default="{ stu }">
      <span :class="{ cursed: stu.name == 'Harry' }">
        {{ stu.name }}
      </span>
    </template>
  </StudentList>

  <hr>

  <el-table :data="todoList" stripe border style="width: 100%">
    <el-table-column prop="userId" label="User ID" width="180" />
    <el-table-column prop="id" label="ID" width="180" />
    <el-table-column prop="title" label="Title" />
    <el-table-column prop="completed" label="Status">
      <template #default="slotProps">
        <el-tag type="success" v-if="slotProps.row.completed">Complete</el-tag>
        <el-tag type="danger" v-else>Incomplete</el-tag>
      </template>
    </el-table-column>
  </el-table>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import StudentList from './StudentList.vue'

const list = ref([
  {
    id: 1,
    name: 'Harry'
  },
  {
    id: 2,
    name: 'Hermione'
  },
  {
    id: 3,
    name: 'Ron'
  }
])

const todoList = ref([])

async function getTodoList() {
  const response = await fetch('https://jsonplaceholder.typicode.com/todos')
  const data = await response.json()
  console.log(data)
  todoList.value = data
}

onMounted(() => {
  getTodoList()
})
</script>

<style scoped>
.cursed {
  color: red;
}
</style>

<!-- Vue 28: Named Slots -->
<!-- <template>
  <BaseLayout>
    <template #header>
      <h1>Here is a page title.</h1>
    </template>
    <template #main>
      <p>A paragraph of the main content.</p>
      <p>And another one.</p>
    </template>
    <template #footer>
      <p>Here is some contact info.</p>
    </template>
  </BaseLayout>
</template>

<script setup>
import BaseLayout from './BaseLayout.vue'
</script>

<style scoped></style> -->

<!-- Vue 27: Slots -->
<!-- <template>
  <AlertBox>
    Invalid username or password! Please try again.
  </AlertBox>
  <AlertBox></AlertBox>
  <AlertBox>
    <h1>
      The request timed out. Please refresh the page and try again.
    </h1>
  </AlertBox>
</template>

<script setup>
import AlertBox from './AlertBox.vue'
</script>

<style scoped></style> -->

<!-- Vue 26: Provide & Inject -->
<!-- <template>
  <h1>Message: {{ message }}</h1>
  <div style="background-color: orange; padding-left: 10px">
    <ComponentA></ComponentA>
  </div>
</template>

<script setup>
import { ref, provide, readonly } from 'vue'
import ComponentA from './ComponentA.vue'

let message = ref('Hello, Provide/inject!')
function updateMessage() {
  message.value = 'Hello, Provide/inject! Updated.'
}
provide('msg', { message, updateMessage })

let count = ref(0)
provide('read-only-count', readonly(count))
</script>

<style scoped></style> -->

<!-- Vue 25: Component V-Model -->
<!--<template>
  <BlogPost v-for="post in posts" :key="post.id" :id="post.id" v-model:blogPostTitle="post.blogPostTitle"
    v-model:blogPostContent="post.blogPostContent" @delete-blog-post="processDeletion"></BlogPost>
</template>

<script setup>
import { ref } from 'vue'
import BlogPost from './BlogPost.vue'
let posts = ref([
  {
    id: 1,
    blogPostTitle: 'What is a muggle in HP world?',
    blogPostContent:
      'A muggle is a person who lacks any sort of magical ability...'
  },
  {
    id: 2,
    blogPostTitle:
      'HP and the Cursed Child Broadway production suspended until April',
    blogPostContent:
      'Adding to the earlier post, the Broadway production of Harry Potter and the Cursed Child has been...'
  },
  {
    id: 3,
    blogPostTitle: 'Potter DIY: Make Your Own “Harry Potter Puppet Pal”',
    blogPostContent:
      'We all remember those iconic YouTube videos of Harry and the gang and probably couldn’t get “The Mysterious...'
  },
  {
    id: 4,
    blogPostTitle: 'Fan Project Brings Life to “Harry Potter” in Translation',
    blogPostContent:
      'It’s no secret that the Harry Potter series is a global phenomenon, having been translated into over 80 languages to date....'
  }
])

function processDeletion(id) {
  let index = posts.value.findIndex((item) => item.id == id)
  posts.value.splice(index, 1)
}
</script>

<style scoped></style> -->

<!-- Vue 24: Component Events -->
<!-- <template>
  <BlogPost v-for="post in posts" :key="post.id" v-bind="post" @delete-blog-post="processDeletion"></BlogPost>
</template>

<script setup>
import { ref } from 'vue'
import BlogPost from './BlogPost.vue'
let posts = ref([
  {
    id: 1,
    blogPostTitle: 'What is a muggle in HP world?',
    blogPostContent:
      'A muggle is a person who lacks any sort of magical ability...'
  },
  {
    id: 2,
    blogPostTitle:
      'HP and the Cursed Child Broadway production suspended until April',
    blogPostContent:
      'Adding to the earlier post, the Broadway production of Harry Potter and the Cursed Child has been...'
  },
  {
    id: 3,
    blogPostTitle: 'Potter DIY: Make Your Own “Harry Potter Puppet Pal”',
    blogPostContent:
      'We all remember those iconic YouTube videos of Harry and the gang and probably couldn’t get “The Mysterious...'
  },
  {
    id: 4,
    blogPostTitle: 'Fan Project Brings Life to “Harry Potter” in Translation',
    blogPostContent:
      'It’s no secret that the Harry Potter series is a global phenomenon, having been translated into over 80 languages to date....'
  }
])

function processDeletion(id) {
  let index = posts.value.findIndex((item) => item.id == id)
  posts.value.splice(index, 1)
}
</script>

<style scoped></style> -->

<!-- Vue 23: Props -->
<!-- <template>
  <BlogPost id="1" blogPostTitle="What is a muggle?"
    blogPostContent="A muggle is a person who lacks any sort of magical ability...">
  </BlogPost>

  <BlogPost id="1" blog-post-title="What is a muggle?"
    blog-post-content="A muggle is a person who lacks any sort of magical ability...">
  </BlogPost>

  <BlogPost :id="blogPostId" :blog-post-title="blogPostTitle" :blog-post-content="blogPostContent"></BlogPost>

  <hr>

  <BlogPost v-for="post in posts" :key="post.id" :id="post.id" :blog-post-title="post.blogPostTitle"
    :blog-post-content="post.blogPostContent"></BlogPost>

  <hr>

  <BlogPost v-for="post in posts" :key="post.id" v-bind="post"></BlogPost>
</template>

<script setup>
import BlogPost from '@/BlogPost.vue'
import { ref } from 'vue'

let blogPostId = ref(2)
let blogPostTitle = ref(
  'HP and the Cursed Child Broadway production suspended until April'
)
let blogPostContent = ref(
  'Adding to the earlier post, the Broadway production of Harry Potter and the Cursed Child has been...'
)

let posts = ref([
  {
    id: 1,
    blogPostTitle: 'What is a muggle in HP world?',
    blogPostContent:
      'A muggle is a person who lacks any sort of magical ability...'
  },
  {
    id: 2,
    blogPostTitle:
      'HP and the Cursed Child Broadway production suspended until April',
    blogPostContent:
      'Adding to the earlier post, the Broadway production of Harry Potter and the Cursed Child has been...'
  },
  {
    id: 3,
    blogPostTitle: 'Potter DIY: Make Your Own “Harry Potter Puppet Pal”',
    blogPostContent:
      'We all remember those iconic YouTube videos of Harry and the gang and probably couldn’t get “The Mysterious...'
  },
  {
    id: 4,
    blogPostTitle: 'Fan Project Brings Life to “Harry Potter” in Translation',
    blogPostContent:
      'It’s no secret that the Harry Potter series is a global phenomenon, having been translated into over 80 languages to date....'
  }
])
</script>

<style scoped></style> -->

<!-- Vue 21: Intro Components -->
<!--<template>
  <ButtonCounter></ButtonCounter>
  <ButtonCounter></ButtonCounter>
  <button-counter></button-counter>

  <hr>

  <div style="background-color: orange; padding: 5px">
    This is the root component.
    <ComponentA></ComponentA>
    <ComponentA></ComponentA>
  </div>
</template>

<script setup>
import ButtonCounter from './ButtonCounter.vue'
import ComponentA from '@/ComponentA.vue'
</script>

<style scoped></style> -->

<!-- Vue 20: Lifecycle Hooks -->
<!-- <template>
  <h1>{{ message }}</h1>
  <div class="card">
    <h2 ref="title">This is the App Component.</h2>
    <h2>Number: {{ number }}</h2>
    <button @click="number++">Increment Number by One</button>
    <button @click="isShow = !isShow">Toggle Component1</button>
    <Component1 v-if="isShow"></Component1>
  </div>
</template>

<script setup>
import {
  ref,
  onBeforeMount,
  onMounted,
  onBeforeUpdate,
  onUpdated,
  onBeforeUnmount,
  onUnmounted,
  watch
} from 'vue'

import Component1 from './Component1.vue'

let message = ref('Hello, Lifecycle Hooks!')
let number = ref(1)
let title = ref(null)
let isShow = ref(true)

console.log('Setup App Component.')

onBeforeMount(() => {
  console.log('App Component is Before Mount.')
  console.log(number.value)
  console.log(title.value)
})
onMounted(() => {
  console.log('App Component is Mounted.')
  console.log(title.value)
})
onBeforeUpdate(() => {
  console.log('App Component is Before Update.')
})
onUpdated(() => {
  console.log('App Component is Updated.')
})
onBeforeUnmount(() => {
  console.log('App Component is Before Unmount.')
})
onUnmounted(() => {
  console.log('App Component is Unmounted.')
})
watch(number, () => {
  console.log('Number Changed!')
})
</script>

<style scoped>
.card {
  background-color: purple;
  color: white;
  padding: 20px 10px;
  margin-bottom: 10px;
}
</style> -->

<!-- Vue 19: Template Refs -->
<!-- <template>
  <div class="card">
    <h1 ref="title">Hello, Template Refs!</h1>
    <input type="text" ref="input">
    <button @click="printDomElements">Print DOM Elements in Console Log</button>
    <button @click="changeTitle">Change Title</button>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'

let title = ref()
const input = ref()

function printDomElements() {
  console.log(title.value)
  console.log(input.value)
}

function changeTitle() {
  title.value.innerText = 'Hello World!'
}

onMounted(() => {
  input.value.focus()
})
</script>

<style scoped>
.card {
  background-color: purple;
  color: white;
  padding: 20px 10px;
  margin-bottom: 10px;
}
</style> -->

<!-- Vue 18: watchEffect -->
<!-- <template>
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
</style> -->

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