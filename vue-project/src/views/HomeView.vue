<template>
  <div>
    <!-- 1. Template Syntax -->
    <p>1a. Text Interpolation: {{ message }}</p>
    <div>1b. Raw HTML: <div v-html="rawHtml"></div></div>
    <button :id="buttonId">1c. Attribute Bindings</button>
    <p>1d. JavaScript Expression: {{ calculateSum(3, 5) }}</p>

    <!-- 4. Computed Properties -->
    <p>4. Computed Property: {{ computedMessage }}</p>

    <!-- 5. Class and Style Bindings -->
    <div :class="toggleClass">5a. Binding HTML class</div>
    <div :style="inlineStyles">5b. Binding Inline Styles</div>

    <!-- 6. List Rendering -->
    <ul>
      <li v-for="(item, index) in list" :key="index">{{ item.name }}</li>
    </ul>

    <!-- 7. Event Handling -->
    <button @click="handleClickInline">7a. Inline Handler</button>
    <button @click="handleClickMethod">7b. Method Handler</button>

    <!-- 8. Form Input Bindings -->
    <input v-model="textInput" type="text" placeholder="Text Input">
    <input v-model.number="numberInput" type="number" placeholder="Number Input">
    <input v-model.trim="trimmedInput" type="text" placeholder="Trimmed Input">
    <textarea v-model="textAreaInput" placeholder="Text Area"></textarea>

    <!-- 9. Watchers -->
    <p>Watched Value: {{ watchedValue }}</p>

    <!-- 10. Components -->
    <child-component :propValue="parentValue" @customEvent="handleChildEvent">
      <template #slotName>
        <p>Slot Content</p>
      </template>
    </child-component>
  </div>
</template>

<script setup>
import { ref, computed, watch, defineProps, defineEmits } from 'vue';

// 1. Template Syntax
const message = ref('Hello, Vue 3!');
const rawHtml = ref('<span style="color: red;">Raw HTML</span>');
const buttonId = ref('my-button');

// 4. Computed Properties
const computedMessage = computed(() => message.value.toUpperCase());

// 5. Class and Style Bindings
const toggleClass = ref('highlight');
const inlineStyles = ref({ color: 'blue', fontSize: '16px' });

// 6. List Rendering
const list = ref([{ name: 'Item 1' }, { name: 'Item 2' }, { name: 'Item 3' }]);

// 8. Form Input Bindings
const textInput = ref('');
const numberInput = ref(0);
const trimmedInput = ref('');
const textAreaInput = ref('');

// 9. Watchers
const watchedValue = ref(0);
watch(watchedValue, (newValue, oldValue) => {
  console.log(`Watched value changed from ${oldValue} to ${newValue}`);
});

// 10. Components
const props = defineProps(['propValue']);
const emits = defineEmits(['customEvent']);
const parentValue = ref('Parent Value');

// Methods
const calculateSum = (a, b) => a + b;

// Event Handling
const handleClickInline = () => alert('Inline handler clicked');
const handleClickMethod = () => alert('Method handler clicked');

// Child Component
const handleChildEvent = () => alert('Child event received');

</script>

<style>
.highlight {
  background-color: yellow;
}
</style>