<template>
    <div>
      <p>Child Component</p>
      <p>{{ propValue }}</p>
      <button @click="emitCustomEvent">Emit Custom Event</button>

      <!-- 10c. Slot: to pass content from the parent component -->
    <slot></slot>
    </div>
  </template>
  
  <script>
  import { defineProps, defineEmits } from 'vue';
  
  //10a. props: 
  export default {
    setup() {
      const props = defineProps({
        propValue: String,
      });
  //10b. emit events: used to trigger a custom event named 'customEvent'
      const emit = defineEmits();
      const emitCustomEvent = () => {
        emit('customEvent', 'Custom Event Data');
      };
  
      return { props, emitCustomEvent };
    },
  };
  </script>
  