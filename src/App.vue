<script setup>
import { ref } from "vue";
import FootballField from "./FootballField.vue";
import PlayerMarker from "./PlayerMarker.vue";
import PlayerInfo from "./PlayerInfo.vue";
import { players } from "./playerData.js";
const playersById = players.reduce((acc, curr) => {
  acc[curr.id] = curr;
  return acc;
}, {});

const formation = [
  ["sanchez", "villa", "messi"],
  ["iniesta", "sergio_busquets", "xavi"],
  ["jordi_alba", "pique", "carles_puyol", "dani_alves"],
  ["victor_valdes"],
];

const selectedPlayer = ref(null);

let targetEl = null;
let namedViewRefs = null;

const runViewTransitionTempEffects = () => {
  const [imgRef, nameRef, ratingRef] = [
    "img",
    ".player-marker__name",
    ".player-marker__rating",
  ].map((selector) => targetEl.querySelector(`:scope ${selector}`));
  imgRef.style.viewTransitionName = "player-photo";
  nameRef.style.viewTransitionName = "player-name";
  ratingRef.style.viewTransitionName = "player-rating";
  namedViewRefs = [imgRef, nameRef, ratingRef];
};
const cleanViewTransitionTempEffects = () => {
  namedViewRefs?.forEach((ref) => (ref.style.viewTransitionName = ""));
};

const updateSelectedPlayer = (playerId, target) => {
  targetEl = target;
  runViewTransitionTempEffects();

  document.startViewTransition(() => {
    cleanViewTransitionTempEffects();
    selectedPlayer.value = playersById[playerId];
  });
};

const closeInfoPopup = () => {
  const transition = document.startViewTransition(() => {
    runViewTransitionTempEffects();
    selectedPlayer.value = null;
  });
  transition.finished.finally(() => {
    cleanViewTransitionTempEffects();
    namedViewRefs = null;
    targetEl = null;
  });
};
</script>
<template>
  <FootballField :class="{ 'is-blurred': selectedPlayer }">
    <ul v-for="line in formation">
      <li
        style="cursor: pointer"
        v-for="playerId in line"
        @click="updateSelectedPlayer(playerId, $event.target)"
      >
        <PlayerMarker :data="playersById[playerId]" />
      </li>
    </ul>
  </FootballField>
  <PlayerInfo
    :data="selectedPlayer"
    v-if="selectedPlayer"
    @close="closeInfoPopup"
  />
</template>
<style lang="scss"></style>
