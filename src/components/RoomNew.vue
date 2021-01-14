<template>
  <div class="room-new pt-3">
    <div class="row">
      <label for="id" class="col">id : </label>
      <input id="id" class="col" v-model='room.id' placeholder="id"><br>
    </div>
    <div class="row">
      <label for="level" class="col">level : </label>
      <input id="level" class="col" v-model='room.level' placeholder="level"><br>
    </div>
    <div class="row">
      <label for="name" class="col">name : </label>
      <input id="name" class="col" v-model='room.name' placeholder="name"><br>
    </div>
    <div class="row">
      <label for="type" class="col">type : </label>
      <input id="type" class="col" v-model='room.type' placeholder="type"><br>
    </div>
    <div class="row">
      <label for="currentTemperature" class="col">currentTemperature : </label>
      <input id="currentTemperature" class="col" v-model='room.currentTemperature' placeholder="currentTemperature"><br>
    </div>
    <div class="row">
      <label for="targetTemperature" class="col">targetTemperature : </label>
      <input id="targetTemperature" class="col" v-model='room.targetTemperature' placeholder="targetTemperature"><br>
    </div>
    <button type="button" class="btn btn-secondary me-2" @click="createRoom">Create</button>
  </div>
</template>

<script>
import axios from 'axios';
import {API_HOST} from '../config';

export default {
  name: 'RoomNew',
  data: function () {
    return {
      room: {
        id: '',
        level: '',
        name: '',
        type: '',
        currentTemperature: '',
        targetTemperature: ''
      }
    }
  },
  methods:{
    async createRoom() {
      let room = {
        'id': parseInt(this.room.id),
        'level': parseInt(this.room.level),
        'name': this.room.name,
        'type': this.room.type,
        'currentTemperature': parseFloat(this.room.currentTemperature),
        'targetTemperature': parseFloat(this.room.targetTemperature)
      }

      console.log(room)
      let response = await axios.post(`${API_HOST}/api/rooms`, room);
      let updatedRoom = response.data;
      this.$emit('room-new', updatedRoom);
    }
  }
}
</script>

<style scoped>
.room-new {
  text-align: left;
}
</style>