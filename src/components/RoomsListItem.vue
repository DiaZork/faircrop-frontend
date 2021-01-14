<template>
  <div class="room border border-secondary rounded p-2 mb-2" :class="{expanded: isExpanded}">
    <div class="top-row d-flex" @click="toggleExpand">
      <div class="room-name fw-bold pe-3">{{ room.name }}</div>
      <div class="room-level text-muted pe-3">{{ room.level }}</div>
      <div class="room-type text-muted pe-3">{{ room.type ? room.type : '--' }}</div>
      <div class="room-current-temperature temperature pe-3">{{room.currentTemperature?room.currentTemperature:'--' }}</div>
      <div class="room-target-temperature temperature pe-3">{{room.targetTemperature?room.targetTemperature: "--" }}</div>

      <div class="expand-button ms-auto">
        {{ isExpanded ? '&#9660;' : '&#9658;' }}
      </div>
    </div>
    <template v-if="isExpanded">
      <hr/>
      <div class="details d-flex">
        <button type="button" class="btn btn-danger" @click="deleteRoom">Delete room</button>
      </div>
    </template>
  </div>
</template>

<script>
import axios from "axios";
import {API_HOST} from "@/config";

export default {
  name: "RoomsListItem",
  props: ['room'],
  data: function () {
    return {
      isExpanded: false
    }
  },
  computed: {
    isRoomOpen: function () {
      return this.room.status === 'OPEN';
    }
  },
  methods: {
    toggleExpand() {
      this.isExpanded = !this.isExpanded;
    },
    async deleteRoom() {
      let response = await axios.delete(`${API_HOST}/api/rooms/${this.room.id}`);
      //let updatedRoom = response.data;
      if (response.status === 200) {
        this.$emit('room-delete', this.room);
      }
    }
  }
}
</script>

<style scoped>
  .temperature::after {
    content: '°C';
  }
</style>