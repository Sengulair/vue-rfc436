<script setup lang="ts" generic="T extends InputType">
export type InputType = 'text' | 'number';
type ComponentReturnType<T extends InputType = 'text'> 
	= T extends 'text' ? string : number;

type Props = {
	type: T;
	modelValue: ComponentReturnType<T>;
}

const props = withDefaults(
	defineProps<Props>(),
	{ type: 'text' },
);

const emit = defineEmits<{ 
	(e: 'update:modelValue', value: ComponentReturnType<T>): void;
}>();

const onInput = (e: Event) => {
	const inputValue = (e.target as HTMLInputElement).value;
	const value = props.type === 'text' ? inputValue as ComponentReturnType<T> : parseFloat(inputValue) as ComponentReturnType<T>;
	emit('update:modelValue', value);
}
</script>

<template>
	<input :value="modelValue" :type="type" @input="onInput"/>
</template>
