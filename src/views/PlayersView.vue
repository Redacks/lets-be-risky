<script setup lang="ts">
import CustomButton from "../components/CustomButton.vue";
import { ref } from "vue";
import { usePlayerStore } from "@/stores/playerStore";
import AddPlayer from "@/components/AddPlayer.vue";
import { storeToRefs } from "pinia";
import DeleteIcon from "virtual:icons/mingcute/delete-2-fill";
import UserAddIcon from "virtual:icons/mingcute/user-add-2-fill";

const playerStore = usePlayerStore();
const { players } = storeToRefs(playerStore);
const newPlayerDialogOpen = ref(false);
</script>
<template>
  <div class="flex flex-1 flex-col text-center font-madimiOne text-customWhite">
    <h2 class="mb-6 text-4xl">Spieler</h2>
    <div class="flex flex-1 flex-col">
      <div v-if="players.length != 0" class="flex flex-col gap-4 px-10">
        <div
          class="shadow-gray flex items-center justify-between rounded-lg bg-gray-700 px-4 py-2 text-xl shadow-md"
          v-for="player in players"
          :key="player"
        >
          {{ player }}
          <button
            class="transition-transform hover:scale-110"
            @click="playerStore.removePlayer(player)"
          >
            <DeleteIcon class="h-6 w-6 text-customRed" />
          </button>
        </div>
      </div>
      <AddPlayer v-if="newPlayerDialogOpen" @close="newPlayerDialogOpen = false" />
      <div class="my-4 mt-auto flex flex-col gap-6 pt-6">
        <button class="mx-auto" @click="newPlayerDialogOpen = true">
          <CustomButton text="Spieler hinzufügen" color="green">
            <UserAddIcon class="mr-2" />
          </CustomButton>
        </button>
        <RouterLink to="/" class="mx-auto">
          <CustomButton text="Zurück" color="transparent" />
        </RouterLink>
      </div>
    </div>
  </div>
</template>
