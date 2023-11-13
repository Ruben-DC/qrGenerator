<script setup>
	import { ref } from 'vue';
	const emit = defineEmits(['generateQR']);

	const qrInput = ref('');
	const handleValidate = () => {
		if (qrInput.value !== '') {
			emit('generateQR', qrInput.value);
			qrInput.value = '';
		}
	};
</script>

<template>
	<div class="input__wrapper">
		<label for="qrInput" class="input__label">Generate a QR Code</label>

		<input
			id="qrInput"
			class="input__input"
			type="text"
			placeholder="Generate a QR Code"
			v-model="qrInput"
			@keydown.enter="handleValidate"
		/>

		<button class="input__button" @click="handleValidate">Generate</button>
	</div>
</template>

<style lang="scss" scoped>
	@import '../assets/styles/mixins';

	.input {
		&__wrapper {
			display: flex;
			flex-direction: row;
			justify-content: center;
			flex-wrap: wrap;
			gap: 1rem;

			width: 100%;
		}

		&__label {
			position: absolute;
			top: -9999px;
		}

		&__input {
			@include border-rounded();

			max-width: 400px;
			width: 100%;
			padding: 5px 20px;

			background: none;
		}

		&__button {
			@include border-rounded();

			padding: 5px 20px;

			background: none;
			cursor: pointer;
			transition: background 0.2s ease-in-out;

			&:hover {
				background: $black-2;
			}
		}
	}
</style>
