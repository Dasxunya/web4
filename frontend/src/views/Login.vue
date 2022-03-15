<template>
  <div id="login-body">

    <div class="header">
      <div>
        <p>Шаповалова Дарья Сергеевна P3230</p>
        <p>Вариант 30017</p>
      </div>
    </div>

    <div class="container">
      <div class="screen">
        <div class="screen__content">

          <div id="wrapper">
            <form id="signin">
              <input type="text" autocomplete="false" required id="user" name="user" placeholder="Имя пользователя" v-model.trim="login"/>
              <input type="password" autocomplete="false" required id="pass" name="pass" placeholder="Пароль" v-model.trim="password"/>
              <a id="forError" style="font-size: 10px; font-style: oblique; color: #ffb994"></a>
              <button type="submit" @click="loging">&#xf0da;</button>
            </form>
          </div>



          <div class="social-login">
            <a href="/" @click="register">регистрация</a>
          </div>
        </div>


        <!--для фоновых рисунков-->
        <div class="container__content">

        </div>




        <div class="screen__background">


          <span class="screen__background__shape screen__background__shape1"></span>
          <span class="screen__background__shape screen__background__shape3"></span>
          <span class="screen__background__shape screen__background__shape4"></span>

          <!--чел-->
          <span class="screen__background__shape screen__background_shape6"></span>
          <!--Шляпа-->
          <span class="screen__background__shape screen__background__shape2"></span>
          <span class="screen__background__shape screen__background__shape5"></span>


          <div class="container1">
            <div class="moon"></div>
            <div class="cloud-container">
              <div class="cloud"></div>
              <div class="cloud"></div><div class="cloud"></div><div class="cloud"></div><div class="cloud"></div>
            </div> <!--end .cloud-container-->

            <div class="stars">
              <div class="star"></div> <div class="star"></div> <div class="star"></div> <div class="star"></div> <div class="star"></div> <div class="star"></div> <div class="star"></div>
            </div>
            <div class="mountain"></div>
            <div class="train-container">
              <div class="train">

                <div class="train-car">
                  <div class="windows">
                    <div class="w-left"></div>
                    <div class="w-right"></div>
                  </div>
                  <div class="door"></div>
                  <div class="windows">
                    <div class="w-left"></div>
                    <div class="w-right"></div>
                  </div>
                </div>


                <div class="train-car end-car">
                  <div class="door"></div>
                  <div class="windows">
                    <div class="w-left"></div>
                    <div class="w-right"></div>
                    <div class="end-car-window"></div>
                  </div>
                </div>
              </div><!-- end .train-->


              <div class="train-track">
                <div class="ledge"></div>
                <div class="pillar">
                  <div class="pillar-left"></div>
                  <div class="pillar-middle"></div>
                  <div class="pillar-right"></div>
                </div> <!--end .pillar-->

              </div><!--end .train-track-->
            </div> <!--end .train-container-->
          </div> <!--end .container1-->

        </div> <!--end .screen_background-->

      </div> <!--end .screen-->


    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'Login',
  data() {
    return {
      login: "",
      password: ""
    }
  },
  methods: {
    loging(e) {
      e.preventDefault();
      axios.post('http://localhost:8083/api/user/auth', {
        login: this.login,
        password: this.password
      }).then(response => {
        localStorage.setItem("jwt", response.data);
        this.$router.push({name: 'main'});
      }).catch(error => {
        document.getElementById("forError").innerText = error.response.data;
      })
    },
    register(e) {
      e.preventDefault();
      axios.put('http://localhost:8083/api/user/auth', {
        login: this.login,
        password: this.password
      }).then(() => {
        document.getElementById("forError").innerText = "Вы успешно зарегистрированы";
      }).catch(error => {
        document.getElementById("forError").innerText = error.response.data;
      })
    }
  }
}
</script>

<style>
@import "../assets/header.css";
@import "../assets/login.css";
</style>
