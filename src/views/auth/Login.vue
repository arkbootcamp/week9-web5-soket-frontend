<template>
  <div class="container">
    <h1>Halaman login</h1>
    <form action="">
      <div class="form-group">
        <label for="room">Room</label>
          <select class="form-control" name="room" id="room" v-model="room">
            <option value="javascript">Javascript</option>
            <option value="php">PHP</option>
            <option value="golang">Golang</option>
          </select>
      </div>
      <div class="form-group">
        <label for="username">Username</label>
        <input class="form-control" type="text" v-model="username" id="username">
      </div>
      <button class="btn btn-primary" @click="handleLogin">Masuk</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'Login',
  data () {
    return {
      room: null,
      username: ''
    }
  },
  methods: {
    handleLogin () {
      this.$router.push({ name: 'Room', query: { room: this.room, username: this.username } })
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
