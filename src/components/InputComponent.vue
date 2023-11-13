<script setup>
	import { ref } from 'vue';
	const emit = defineEmits(['generateQR']);

	const qrInput = ref('');
	const handleValidate = () => {
		if (qrInput.value !== '') {
			emit('generateQR', {
				value: qrInput.value,
				backgroundColor: backgroundColor.value,
				opacity: opacity.value,
				foregroundColor: foregroundColor.value,
			});

			qrInput.value = '';
		}
	};

	const backgroundColor = ref('#ffffff');
	const foregroundColor = ref('#000000');
	const opacity = ref(1);

	const detailsIsOpen = ref(false);
</script>

<template>
	<div class="input__wrapper">
		<div v-if="detailsIsOpen" class="input__details__wrapper">
			<label for="backgroundColor">Couleur de fond :</label>
			<input
				v-model="backgroundColor"
				type="color"
				id="backgroundColor"
				class="input__details__background-color"
			/>

			<div class="input__details__opacity__wrapper">
				<label for="qrOpacity">Opacité du fond :</label>
				<input
					v-model="opacity"
					type="range"
					min="0"
					max="1"
					step="0.001"
					id="qrBackgroundOpacity"
					class="input__details__opacity__range"
				/>
				<input
					type="number"
					min="0"
					max="1"
					step="0.01"
					v-model="opacity"
					class="input__details__opacity__number"
				/>
			</div>

			<label for="foregroundColor">Couleur du QR code :</label>
			<input
				v-model="foregroundColor"
				type="color"
				id="foregroundColor"
				class="input__details__foreground-color"
			/>
		</div>

		<button @click="detailsIsOpen = !detailsIsOpen" class="input__button">
			+
		</button>

		<label for="qrInput" class="input__label">Value to generate</label>

		<input
			id="qrInput"
			class="input__text"
			type="text"
			placeholder="Générez un QR Code"
			v-model="qrInput"
			@keydown.enter="handleValidate"
		/>

		<button class="input__button" @click="handleValidate">
			Value to generate
		</button>
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

		&__text {
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

		&__details {
			&__wrapper {
				display: flex;
				flex-direction: row;
				justify-content: center;
				align-items: center;
				flex-wrap: wrap;
				gap: 1rem;

				width: 100%;
				@include border-rounded;
			}

			&__background-color,
			&__foreground-color {
				width: 40px;
				height: 40px;
				padding: 0;
				border: 0;
				border-radius: 10px;

				background-color: transparent;
			}

			&__opacity {
				&__wrapper {
					display: flex;
					flex-direction: row;
					justify-content: center;
					align-items: center;
					flex-wrap: wrap;
					gap: 1rem;
				}

				&__range {
					width: 100px;
				}

				&__number {
					width: 70px;

					background: none;
					border: none;
					color: $font-color;
					border-bottom: 1px solid $black-2;
					text-align: center;
				}
			}
		}
	}
</style>
