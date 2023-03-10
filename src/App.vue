<template>
  <div>
    <form>
      <div class="form-group">
        <label for="username">Username</label>
        <input type="text" class="form-control" id="username" v-model="username" required>
      </div>
      <div class="form-group">
        <label for="password">Password</label>
        <input type="password" class="form-control" id="password" v-model="password" required>
      </div>
      <button type="submit" class="btn btn-primary">Login</button>
    </form>
  </div>
</template>

<style>

</style>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      username: '',
      password: '',
      error: null,
    };
  },
  methods: {
    async submitForm() {
      try {
        const response = await axios.post('/api/login.php', {
          username: this.username,
          password: this.password,
        });
        const token = response.data.token;
        // 將JWT令牌存儲在應用程式狀態中
        this.$store.commit('setToken', token);
        // 將用戶重定向到用戶記事本頁面
        this.$router.push('/user');
      } catch (error) {
        this.error = error.response.data.message;
      }
    },
  },
};
</script>