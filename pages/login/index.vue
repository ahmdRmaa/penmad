<template>
  <div class="container d-flex justify-content-center align-items-center vh-100">
    <div class="card" style="width: 20rem;">
      <div class="card-body">
        <h5 class="card-title text-center">Login</h5>
        <form @submit.prevent="login">
          <div class="mb-3">
            <label for="username" class="form-label">Username</label>
            <input 
              type="text" 
              id="username" 
              class="form-control" 
              v-model="username" 
              required
            />
          </div>
          <div class="mb-3">
            <label for="password" class="form-label">Password</label>
            <input 
              type="password" 
              id="password" 
              class="form-control" 
              v-model="password" 
              required
            />
          </div>
          <div class="mb-3">
            <button type="submit" class="btn btn-primary w-100">Login</button>
          </div>
          <div v-if="errorMessage" class="alert alert-danger" role="alert">
            {{ errorMessage }}
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: '',
      password: '',
      errorMessage: '',
    };
  },
  methods: {
    login() {
      const validUsername = 'admin';
      const validPassword = '123';

      // Validasi login
      if (this.username === validUsername && this.password === validPassword) {
        this.$router.push('/dasbor');  // Arahkan ke halaman dashboard setelah login berhasil
      } else {
        this.errorMessage = 'Username atau password salah!';
      }
    },
  },
};
</script>

<style scoped>
.card {
  width: 100%;
  max-width: 400px;
}
</style>
