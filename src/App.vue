<template>
  <div>
    <!--11. Router: to manage the navigation of each page such as home and about page -->
    <router-link to="/">Home</router-link>
    <router-link to="/about">About</router-link>
    <!-- 1a. Text Interpolation: to diplay the value of the 'message' variable -->
    <p>{{ message }}</p>

    <!-- 1b. Raw HTML: to render raw HTML stored in the 'rawHtml variable within a 'div' -->
    <div v-html="rawHtml"></div>

    <!-- 1c. Attribute Bindings: to bind the 'id' attribute of 'div' to the 'elementId' variable -->
    <div :id="elementId"></div>

    <!-- 1d. JavaScript expressions inside syntax: to calculates a sum of '10' and '5' and display it in a paragraph -->
    <p>{{ calculateSum(10, 5) }}</p>

    <!-- 5. Class and Style Bindings: to bind class and style properties of a 'div' using 'classObject' and 'styleObject' -->
    <div :class="classObject" :style="styleObject"></div>

    <!-- List Rendering -->
    <!-- 6c. v-for on <template>:  -->
    <ul>
      <li v-for="item in items" :key="item.id">{{ item.name }}</li>
    </ul>

    <!-- 6a. v-for with an Object:  -->
    <ul>
      <li v-for="(value, key) in objectData" :key="key">{{ key }}: {{ value }}</li>
    </ul>

    <!-- 6b. v-for with a Range:  -->
    <ul>
      <li v-for="number in range(10, 16)" :key="number">{{ number }}</li>
    </ul>




    <!-- 7a. Inline handlers: to listens for a click event on a button and triggers the handleClick method -->
    <button @click="handleClick">Click Me</button>


    <!-- 8b. Form Input Bindings: to input elements to reactive variables (textInput, numericInput, and trimmedInput) using v-model -->
    <input v-model="textInput" type="text" />
    <input v-model.number="numericInput" type="number" />
    <input v-model.trim="trimmedInput" type="text" />

    <!-- 8a. v-model with checkboxes: a form control that allows users to select multiple options from a set of choices -->
    <label>
      <input type="checkbox" v-model="isChecked" /> Checkbox
    </label>

    <!-- 8a. v-model with radio buttons: a form control that allows users to select single options from a set of choices. -->
    <label>
      <input type="radio" value="option1" v-model="selectedOption" /> 1
    </label>
    <label>
      <input type="radio" value="option2" v-model="selectedOption" /> 2
    </label>

    <!-- Components -->
    <ChildComponent :propValue="message" @customEvent="handleCustomEvent"></ChildComponent>
  </div>
</template>

<!-- 3. Reactivity Fundamentals -->
<!-- ref(): it allows to create reactive variables-->
<!-- <script setup>: to simplifies the setup of a Vue component script section-->

<script setup>
import { ref, computed, watch } from 'vue';
import ChildComponent from './components/ChildComponent.vue';

const message = ref('This text is using text interpolation!');
const rawHtml = ref('<span style="color: red;">Raw HTML</span>');
const elementId = 'dynamicId';
const textInput = ref('');
const numericInput = ref(0);
const trimmedInput = ref('');
const items = ref([
  { id: 1, name: 'Item 1' },
  { id: 2, name: 'Item 2' },
]);
const classObject = computed(() => ({ active: true, 'text-danger': false }));
const styleObject = computed(() => ({ color: 'blue', fontSize: '18px' }));

//2. Methods: to calculate the sum of two number
const calculateSum = (a, b) => a + b;

//7b. Method handlers: event handlers defined as methods in the component <script setup>.
const handleClick = () => {
  message.value = 'Button Clicked';
};

//2. Methods: to handle a custom event emmited by the component
const handleCustomEvent = (data) => {
  console.log('Custom Event:', data);
};

//4. computed properties: to calculate the sum of numericInput and 10
const sumResult = computed(() => {
  return numericInput.value + 10;
});

// Watcher for the sumResult computed property
watch(sumResult, (newValue) => {
  console.log('Sum Result Changed:', newValue);
});

//9. Watchers: listen to changes in the textInput variable
watch(textInput, (newValue) => {
  console.log('Text Input:', newValue);
});


const isChecked = ref(false);
const selectedOption = ref('option1');

// Data as an object for v-for
const objectData = {
  FirstName: 'Darren',
  LastName: 'Sunandar',
  Age: 19,
};

// Function to generate a range of numbers
const range = (start, end) => {
  return Array.from({ length: end - start }, (_, index) => start + index);
};

</script>
