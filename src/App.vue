<script setup lang="ts">
import { ref } from 'vue';

import AppInput from './components/AppInput.vue'
import AppInputGeneric from './components/AppInputGeneric.vue'

const string = ref('');
const number = ref(0);
const log = (value: string | number) => {
	console.log(value);
}
</script>

<template>
  <AppInputGeneric :model-value="string" type="text" @update:model-value="(arg) => log(arg)" />
	<AppInputGeneric :model-value="string" type="text" @update:modelValue="(arg) => log(arg)" />

	<AppInputGeneric :model-value="number" type="number" @update:model-value="(arg) => log(arg)" />
	<AppInputGeneric :model-value="number" type="number" @update:modelValue="(arg) => log(arg)" />

	<AppInput :model-value="number" type="number" @update:model-value="(arg) => log(arg)" />
	<AppInput :model-value="string" type="text" @update:modelValue="(arg) => log(arg)" />
</template>