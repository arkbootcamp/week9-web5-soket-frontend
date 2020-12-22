<template>
  <div class="container">
    <div class="row">
      <div class="col-4">
      </div>
      <div class="col-8">
      <ul class="list-group">
  <li class="list-group-item active" >Nama ROOM :  {{$route.query.room}}</li>
  <li class="list-group-item" v-for="(message, index ) in messages" :key="index">{{message}}</li>
</ul>
    <div class="input-group mb-3">
  <input type="text" class="form-control" v-model="inputMessage" @keypress.enter="handleClick" placeholder="input message">
  <div class="input-group-append">
    <button @click="handleClick" class="btn btn-outline-secondary" type="button" id="button-addon2">Kirim</button>
  </div>
</div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Room',
  props: ['socket'],
  data () {
    return {
      messages: [],
      inputMessage: '',
      room: ''
    }
  },
  methods: {
    handleClick () {
      this.socket.emit('reciverMessage', { room: this.room, message: this.inputMessage })
      this.inputMessage = ''
    }
  },
  mounted () {
    const username = this.$route.query.username
    const room = this.$route.query.room
    this.room = room
    this.socket.emit('initialUser', { username: username, room: room })
    this.socket.on('kirimKembali', (data) => {
      this.messages.push(data)
    })
  }
}
</script>

<style lang="scss" scoped>

</style>
