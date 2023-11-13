<script setup>
	import InputComponent from './components/InputComponent.vue';
	import QrCanvas from './components/QrCanvas.vue';
	import { ref } from 'vue';

	const qrValue = ref('');
	const backgroundColor = ref('#ffffff');
	const foregroundColor = ref('#000000');
	const opacity = ref(1);

	const handleGnerateQR = (infos) => {
		qrValue.value = infos.value;
		backgroundColor.value = infos.backgroundColor;
		opacity.value = infos.opacity;
		foregroundColor.value = infos.foregroundColor;
	};
</script>

<template>
	<InputComponent @generateQR="handleGnerateQR" />

	<QrCanvas
		:qrValue="qrValue"
		:background="backgroundColor"
		:opacity="opacity"
		:foreground="foregroundColor"
	/>
</template>

<style lang="scss" scoped></style>
