<template>
  <div class="kotak_login">
    <p class="tulisan_login">Silahkan login</p>

    <label>Username</label>
    <input
      type="text"
      name="username"
      v-model="form.username"
      class="form_login"
      placeholder="Username atau "
    />
    <label>Password</label>
    <input
      type="password"
      name="password"
      v-model="form.password"
      class="form_login"
      placeholder="Password .."
    />

    <input type="button" @click="login()" class="tombol_login" value="LOGIN" />
    <p style="text-align: center">
      <a href="/register"> Silahkan Registerasi</a>
    </p>
  </div>
</template>
<script >
import axios from "axios";
export default {
  name: "Login",
  data() {
    return {
      form: {
        username: "",
        password: "",
      },
      users: {},
    };
  },
  methods: {
    async getUser() {
      const user = await axios.get("http://localhost:3000/users");
      this.users = user.data;
    },
    login() {
      const login = this.users.find(
        (data) =>
          data.username === this.form.username &&
          data.password === this.form.password
      );
      if (login === undefined) {
        alert("Username Or Password Not Found");
      } else {
        var convertToString = JSON.stringify(login);
        sessionStorage.setItem("USER_DATA", convertToString);
        this.$router.push("/");
        window.location.reload();
      }
    },
  },
  mounted() {
    this.getUser();
  },
};
</script>
<style>
h1 {
  text-align: center;
  /*ketebalan font*/
  font-weight: 300;
}
.tulisan_login {
  text-align: center;
  /*membuat semua huruf menjadi kapital*/
  text-transform: uppercase;
}
.kotak_login {
  width: 350px;
  background: rgb(83, 224, 64);
  /*meletakkan form ke tengah*/
  margin: 80px auto;
  padding: 30px 20px;
}
label {
  font-size: 11pt;
}
.form_login {
  /*membuat lebar form penuh*/
  box-sizing: border-box;
  width: 100%;
  padding: 10px;
  font-size: 11pt;
  margin-bottom: 20px;
}
.tombol_login {
  background: #3373ff;
  color: white;
  font-size: 11pt;
  width: 100%;
  border: none;
  border-radius: 3px;
  padding: 10px 20px;
}
.link {
  color: #232323;
  text-decoration: none;
  font-size: 10pt;
}
</style>