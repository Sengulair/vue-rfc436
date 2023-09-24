<script setup lang="ts" generic="T extends InputType">
export type InputType = 'text' | 'number';
type ComponentReturnType<T extends InputType = 'text'> 
	= T extends 'text' ? string : number;

type Props = {
	type: T;
	modelValue: ComponentReturnType<T>;
  anotherProp?: string;
}

/** 1st example of defining generics withDefaults */
const props = withDefaults(
	defineProps<Props>(),
  { 
    type: 'text',
    anotherProp: 'test',
  }
  /* Below not working either */
	// { 
  //   type: 'text' as T,
  //   anotherProp: 'test',
  // },
);

/** 2nd example of defining generics withDefaults */
// const props = withDefaults(
// 	defineProps<Props>(),
// 	{ anotherProp: 'test' },
// );

/** 3rd example with JS syntax destructuring props and assigning default */
// const { type = 'text', anotherProp = 'test' } = defineProps<Props>();

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
	<input :value="modelValue" :title="props.anotherProp" :type="props.type" @input="onInput"/>
  <!-- Uncomment below for 3rd example -->
  <!-- <input :value="modelValue" :title="anotherProp" :type="type" @input="onInput"/> -->
</template>
