<template>
    <section class="vh-100" >
        <div class="container py-5">
            <div class="row d-flex justify-content-center align-items-center h-100">
                <div class="card shadow-2-strong" style="border-radius: 1rem; border-color:black ">
                    <div class="card-header text-center">
                        <h3>Đăng ký</h3>
                    </div>
                    <div class="card-body text-center justify-content-center">
                        <div class="form-outline mb-4">
                            <label for="name">Tên người dùng</label>
                            <input type="text" id="name" v-model="name">
                        </div>
                        <div class="form-outline mb-4">
                            <label for="email">Tên tài khoản</label>
                            <input type="text" id="email" v-model="email">
                        </div>
                        <div class="form-outline mb-4 ">
                            <label for="password">Mật khẩu</label>
                            <input type="password" id="password" v-model="password">
                        </div>
                        <div class="row justify-content-around">
                            <button @click="signup" class="btn btn-primary">Đăng ký</button>
                            <button class="btn btn-primary">
                                <router-link to="/" class="text">Quay lại</router-link>
                            </button>
                        </div>
                        <p class="mt-3">{{ error }}</p>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>
<script>
import axios from "axios";

export default {
    name: "register",
    data() {
        return {
            name: "",
            email: "",
            password: "",
            error: ""
        };
    },
    methods: {
        signup() {
            let newUser = {
                name: this.name,
                email: this.email,
                password: this.password
            };
            axios.post("http://localhost:3000/signup", newUser)
                .then(() => {
                    this.error = "",
                        alert("Đăng ký thành công, mời bạn đăng nhập!");
                    this.$router.push("/login");
                })
                .catch(() => {
                    if(this.email == "") {
                        this.error = "Vui lòng nhập đầy đủ thông tin";
                    }
                    else {
                        this.error = "Tên tài khoản không được sử dụng";
                    }
                });
        }
    }
}
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
  margin-left: 68px;
}
.form-outline input[type="text"] {
  background: #fff;
  outline: none;
  border-radius: 40px;
  border: solid 2px grey;
  height: 32px;
  margin-left: 40px;
}
.form-outline #name {
  background: #fff;
  outline: none;
  border-radius: 40px;
  border: solid 2px grey;
  height: 32px;
  margin-left: 24px;
}
button .text {
    text-decoration: none;
    color: #fff;
}
.card-body p {
    color: red;
}
</style>