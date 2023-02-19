<template>
	<div class="player-marker__wrapper">
		<div class="player-marker__image-and-rating">
			<img :src="getImgUrl()" />
			<span class="player-marker__rating">
				{{ data.rating }}
			</span>
		</div>
		<span class="player-marker__name">
			{{ data.name }}
		</span>
	</div>
</template>
<script setup>
const props = defineProps(["data"]);
const getImgUrl = () =>
	new URL(`./images/${props.data.id}.png`, import.meta.url).href;
</script>
<style lang="scss">
.player-marker {
	&__wrapper {
		display: flex;
		flex-direction: column;
		align-items: center;
		position: relative;
		font-size: 0.65rem;
		pointer-events: none;
	}
	&__name {
		font-weight: bold;
		font-size: 0.8rem;
		text-shadow: 1px 1px 2px rgba(black, 0.5);
		contain: layout;
		white-space: nowrap;
	}
	&__image-and-rating {
		position: relative;
		img {
			max-width: 5cqw;
			border-radius: 10px;
			contain: layout;
			@media (orientation: portrait) {
				max-width: 8cqw;
			}
			@media only screen and (max-width: 600px) {
				max-width: 12cqw;
			}
		}
	}
	&__rating {
		position: absolute;
		bottom: 0px;
		left: -14px;
		font-weight: bold;
		transform: translateX(-20%);
		text-shadow: 1px 1px 2px rgba(black, 0.5);
		contain: layout;
	}
}
</style>
