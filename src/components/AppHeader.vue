<template>
    <nav class="navbar navbar-expand navbar-dark bg-dark">
        <a href="/login" class="navbar-brand">Ứng dụng Quản lý danh bạ</a>
        <div class="mr-auto navbar-nav">
            <i class="nav-item">
                <router-link :to="{ name: 'contactbook' }" class="nav-link">
                    Danh bạ
                    <i class="fas fa-address-book"></i>
                </router-link>
            </i>
            <i class="nav-item" >
                <router-link to="/" class="nav-link">
                    <b>{{ name }}</b>
                    <i class="fa-solid fa-user"></i>
                </router-link>
            </i> 
            <i class="nav-item" >
                <router-link to="/login" class="nav-link" @click="logout">
                    <i class="fa-solid fa-right-from-bracket"></i>
                </router-link>
            </i> 
        </div>
    </nav>
</template>
<script>
import axios from "axios";

export default {
    data() {
        return {
            name: ""
        };
        isVisible: false
    },
    mounted() {
        axios.get("http://localhost:3000/user", { headers: { token: localStorage.getItem("token") } })
            .then(res => {
                this.name = res.data.user.name;
            });
    },
    methods: {
        logout() {
            alert("Bạn đã đăng xuất khỏi ứng dụng!");
            localStorage.clear();
            // this.$router.go("/login");
        },
        hidden() {

        }
    }
};
</script>