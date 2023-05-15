<script setup lang="ts">
export type InputType = 'text' | 'number';
type ReturnType<T extends InputType = 'text'> 
	= T extends 'text' ? string : number;

type Props = {
	type: InputType;
	modelValue: ReturnType<InputType>;
}

const { type = 'text' } = defineProps<Props>();
const props = withDefaults(
	defineProps<Props>(), 
	{ type: 'text' },
);

const emit = defineEmits<{ 
	(e: 'update:modelValue', value: ReturnType<InputType>): void;
}>();

const onInput = (e: Event) => {
	const inputValue = (e.target as HTMLInputElement).value;
	const value = type === 'text' ? inputValue as ReturnType<InputType> : parseFloat(inputValue) as ReturnType<InputType>;
	emit('update:modelValue', value);
}
</script>

<template>
  <input :type="type" @input="onInput"/>
</template>
