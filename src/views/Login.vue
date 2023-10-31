<template>
    <h1>CHÀO MỪNG BẠN ĐẾN VỚI ỨNG DỤNG QUẢN LÝ DANH BẠ</h1>
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
                            <input type="text" id="email" v-model="email" @blur="validate()" :class="{'is-invalid':error.email}">
                            <div class="invalid-feedback" v-if="error.email">
                                {{ error.email }}
                            </div>
                        </div>
                        <div class="form-outline mb-4 ">
                            <label for="password">Mật khẩu</label>
                            <input type="password" id="password" v-model="password" @blur="validate()" :class="{'is-invalid':error.password}">
                            <div class="invalid-feedback" v-if="error.password">
                                {{ error.password }}
                            </div>
                        </div>
                        <button @click="login" class="btn btn-primary">Đăng nhập</button>
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
            error: {
                email:"",
                password:""
            }
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
                        this.$router.push("/contact");
                    }
                })
        },
        validate() {
            let isValid = true;
            this.error = {
                email: "",
                password: "",
            };
            if(!this.email) {
                this.error.email = "tên tài khoản không được rỗng";
                isValid = false;
            };
            if(!this.password) {
                this.error.password = "mật khẩu là bắt buộc";
                isValid = false;
            };
            return isValid;
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
  /* border-radius: 40px; */
  border: solid 2px grey;
  height: 32px;
  margin-left: 30px;
}
.form-outline input[type="text"] {
  background: #fff;
  outline: none;
  /* border-radius: 40px; */
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
