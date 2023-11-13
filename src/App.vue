<script setup>
	import InputComponent from './components/InputComponent.vue';
	import QrCanvas from './components/QrCanvas.vue';
	import { ref } from 'vue';

	const qrValue = ref('');
	const handleGnerateQR = (value) => {
		qrValue.value = value;
	};
</script>

<template>
	<InputComponent @generateQR="handleGnerateQR" />
	<QrCanvas :qrValue="qrValue" />
</template>

<style lang="scss" scoped></style>
