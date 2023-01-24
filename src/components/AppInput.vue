<script setup lang="ts" generic="T extends InputType">
import { withDefaults } from 'vue'

export type InputType = 'text' | 'number';

type ReturnType<T extends InputType = 'text'> 
	= T extends 'text' ? string : number;

const props = withDefaults(defineProps<{ type: T }>(), { type: 'text' });

const emit = defineEmits<{ 
	(e: 'update:modelValue', value: ReturnType<T>): void;
}>();

const onInput = (e: Event) => {
	const inputValue = (e.target as HTMLInputElement).value;
	const value = props.type === 'text' ? inputValue as ReturnType<T> : parseFloat(inputValue) as ReturnType<T>;
	emit('update:modelValue', value);
}
</script>

<template>
  <input :type="type" @input="onInput"/>
</template>
