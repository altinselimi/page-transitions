<script setup>
import { onMounted, ref, computed } from "vue";
import { playerInfo } from "./playerData.js";

const props = defineProps(["data"]);
defineEmits(["close"]);

const getImgUrl = () =>
	new URL(`./images/${props.data.id}.png`, import.meta.url).href;
const playerInfoRef = ref(null);
onMounted(() => {
	playerInfoRef.value?.focus();
});
const firstAndLastName = computed(() => props.data.full_name.split(" "));
</script>
<template>
	<div
		class="player-info__wrapper"
		tabindex="-1"
		ref="playerInfoRef"
		@blur="$emit('close')"
	>
		<div class="player-info__name-and-photo">
			<div>
				<h2>
					{{ data.name }}
				</h2>
				<div class="player-info__rating">
					{{ data.rating }}
				</div>
			</div>
			<img :src="getImgUrl()" />
		</div>
		<ul>
			<li v-for="stat in playerInfo[data.id]">
				<span>
					{{ stat.label }}
				</span>
				<span>
					{{ stat.value }}
				</span>
			</li>
		</ul>
	</div>
</template>
<style lang="scss">
.player-info {
	&__wrapper {
		position: fixed;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		background-color: rgba(white, 0.8);
		z-index: 4;
		border-radius: 20px;
		color: black;
		padding: 20px 30px;
		border: solid 1px whitesmoke;
		outline: none;
		box-shadow: 0px 0px -4px 2px black;
		max-width: 450px;
		width: 50vw;
		min-width: 350px;
		@media only screen and (max-width: 400px) {
			max-width: 300px;
			min-width: 300px;
		}
		ul {
			display: flex;
			flex-direction: column;
		}
		li {
			display: inline-flex;
			border-bottom: solid 1px rgba(black, 0.05);
			padding: 10px 0px;
			span:first-child {
				margin-right: 30px;
			}
			span:last-child {
				margin-left: auto;
				font-weight: bold;
			}
			&:last-child {
				border-bottom: none;
			}
		}
	}
	&__name-and-photo {
		display: flex;
		align-items: flex-start;
		margin-bottom: 20px;
		font-size: 1.5rem;
		img {
			max-width: 80px;
			border-radius: 20px;
			margin-left: auto;
			background-color: rgba(black, 0.1);

			view-transition-name: player-photo;
			contain: layout;
		}
		h2 {
			view-transition-name: player-name;
			contain: layout;
			margin: 0px;
			line-height: normal;
		}
	}
	&__rating {
		view-transition-name: player-rating;
		contain: layout;
		width: fit-content;
	}
}
</style>
