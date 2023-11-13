<script setup>
	import DownloadIcon from './icons/DownloadIcon.vue';
	import QRious from 'qrious';
	import { ref, watch } from 'vue';

	const props = defineProps({
		qrValue: {
			type: String,
			default: 'https://qr.rubendc.fr',
		},
		background: {
			type: String,
			default: 'white',
		},
		foreground: {
			type: String,
			default: 'black',
		},
		opacity: {
			type: Number,
			default: 1,
		},
	});

	const qrCanvas = ref(null);
	const isQrGenerated = ref(false);

	const generateQR = () => {
		if (qrCanvas.value) {
			new QRious({
				element: qrCanvas.value,
				value: props.qrValue,
				size: 800,

				foreground: props.foreground,
				foregroundAlpha: 1,

				background: props.background,
				backgroundAlpha: props.opacity,
			});

			isQrGenerated.value = true;
		}
	};

	watch(
		[
			() => props.qrValue,
			() => props.foreground,
			() => props.background,
			() => props.opacity,
		],
		() => {
			generateQR();
		}
	);

	const downloadQRCode = () => {
		if (qrCanvas.value !== null && isQrGenerated.value) {
			const dataUrl = qrCanvas.value.toDataURL('image/png');
			const a = document.createElement('a');
			a.href = dataUrl;
			a.download = 'qrcode.png';
			a.click();
		}
	};
</script>

<template>
	<div class="canvas__wrapper">
		<canvas class="canvas" ref="qrCanvas"></canvas>

		<button
			:disabled="!isQrGenerated"
			@click="downloadQRCode"
			class="canvas__download-button"
		>
			<DownloadIcon class="icon" />
		</button>
	</div>
</template>

<style lang="scss" scoped>
	@import '../assets/styles/mixins';
	.canvas {
		@include border-rounded();

		aspect-ratio: 1/1;
		width: 100%;
		background-color: none;

		&__wrapper {
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: center;
			gap: 1rem;

			width: 100%;
		}

		&__download-button {
			position: relative;

			padding: 10px;
			width: 50px;
			height: 50px;

			border: none;
			background: none;
			cursor: pointer;
			transition: all 0.2s ease-in-out;

			.icon {
				position: absolute;
				top: 50%;
				left: 50%;
				transform: translate(-50%, -50%);

				width: 20px;
				height: 20px;

				transition: all 0.2s ease-in-out;
			}

			&:hover {
				.icon {
					top: 40%;
				}
			}
		}
	}
</style>
