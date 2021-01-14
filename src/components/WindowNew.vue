<template>
  <div class="window-new pt-3">
    <div class="row">
      <label for="id" class="col">id : </label>
      <input id="id" class="col" v-model='window.id' placeholder="id"><br>
    </div>
    <div class="row">
      <label for="name" class="col">name : </label>
      <input id="name" class="col" v-model='window.name' placeholder="name"><br>
    </div>
    <div class="row">
      <label for="room_id" class="col">room id : </label>
      <input id="room_id" class="col" v-model='window.room_id' placeholder="room id"><br>
    </div>
    <div class="row">
      <label for="status" class="col">status : </label>
      <div class="col">
        <input id="status" v-model='window.status' type="checkbox" placeholder="status">
        <label for="status">OPEN </label>
      </div>
      <br>
    </div>
    <button type="button" class="btn btn-secondary me-2" @click="createWindow">Create</button>
  </div>
</template>

<script>
import axios from 'axios';
import {API_HOST} from '../config';

export default {
  name: "WindowNew",
  data: function () {
    return {
      window: {
        id: '',
        name: '',
        room_id: '',
        status: false
      }
    }
  },
  methods: {
    async createWindow() {
      let roomResponse = await axios.get(`${API_HOST}/api/rooms/${this.window.room_id}`);
      let room = roomResponse.data
      let window = {
        'id': parseInt(this.window.id),
        'name': this.window.name,
        'room': room,
        'status': this.window.status ? 'OPEN' : 'CLOSED'
      }
      let response = await axios.post(`${API_HOST}/api/windows`, window);
      let updatedWindow = response.data;
      this.$emit('window-new', updatedWindow);
    }
  }
}
</script>

<style scoped>
.window-new {
  text-align: left;
}
</style>