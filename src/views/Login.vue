<template>
    <section class="vh-100" >
        <div class="container py-5">
            <div class="row d-flex justify-content-center align-items-center h-100">
                <div class="card shadow-2-strong" style="border-radius: 1rem; border-color:black ">
                    <div class="card-header text-center">
                        <h3>Đăng nhập</h3>
                    </div>
                    <div class="card-body text-center justify-content-center">
                        <div class="form-outline mb-4">
                            <label for="email">Tên tài khoản</label>
                            <input type="text" id="email" v-model="email">
                        </div>
                        <div class="form-outline mb-4 ">
                            <label for="password">Mật khẩu</label>
                            <input type="password" id="password" v-model="password">
                        </div>
                        <div class="row justify-content-around">
                            <button @click="login" class="btn btn-primary">Đăng nhập</button>
                            <button class="btn btn-primary">
                                <router-link to="/" class="text">Quay lại</router-link>
                            </button>
                        </div>
                        <p class="mt-3">{{ error }}</p>
                    </div>
                    <div class="card-footer">
                        <div class="d-flex justify-content-center">
                            <p>
                                Nếu bạn chưa có tài khoản!
                                <router-link to="/signup" class="links"><b>Đăng ký</b></router-link>
                            </p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>
<script>
import axios from 'axios';

export default {
    name: "Login",
    data() {
        return {
            email: "",
            password: "",
            error: ""
        };
    },
    methods: {
        login() {
            let user = {
                email: this.email,
                password: this.password
            };
            axios.post("http://localhost:3000/login", user)
                .then(res => {
                    if(res.status === 200){
                        localStorage.setItem("token", res.data.token);
                        alert("Đăng nhập thành công");
                        this.$router.push("/");
                    }
                })
                .catch(() => {
                    if(this.email == "") {
                        this.error = "Tên tài khoản không được rỗng";
                    }
                    else {
                        this.error = "Tên tài khoản hoặc mật khẩu không đúng";
                    }
                });
        }
    }
};
</script>
<style scoped>
.form-outline label {
  /* color: #fff; */
  margin-right: 10px;
  text-align: right;
}
.form-outline input[type="password"] {
  background: #fff;
  outline: none;
  border-radius: 40px;
  border: solid 2px grey;
  height: 32px;
  margin-left: 24px;
}
.form-outline input[type="text"] {
  background: #fff;
  outline: none;
  border-radius: 40px;
  border: solid 2px grey;
  height: 32px;
}

button .text{
    text-decoration: none;
    color: #fff;
}
p .links {
    text-decoration: none;
}
.card-body p {
    color: red;
}
</style>
