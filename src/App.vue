<script setup lang="ts">
import AppInput from './components/AppInput.vue'

const update = (value: string) => {
	console.log(value);
}
</script>

<template>
  <AppInput :type="'text'" @update:modelValue="update" />
</template>