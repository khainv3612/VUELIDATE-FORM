<template>
  <div id="app">

    <div class="main">

      <section class="signup">
        <!-- <img src="images/signup-bg.jpg" alt=""> -->
        <div class="container">
          <div class="signup-content">
            <form method="POST" id="signup-form" class="signup-form">
              <h2 class="form-title">Create account</h2>
              <div class="form-group">
                <input type="text" class="form-input" name="name" id="name" placeholder="Your Name"/>
              </div>
              <div class="form-group">
                <input type="email" class="form-input" name="email" id="email" placeholder="Your Email"/>
              </div>
              <div class="form-group">
                <input type="text" class="form-input" name="password" id="password" placeholder="Password"/>
                <span toggle="#password" class="zmdi zmdi-eye field-icon toggle-password"></span>
              </div>
              <div class="form-group">
                <input type="password" class="form-input" name="re_password" id="re_password"
                       placeholder="Repeat your password"/>
              </div>
              <div class="form-group">
                <input type="checkbox" name="agree-term" id="agree-term" class="agree-term"/>
                <label for="agree-term" class="label-agree-term"><span><span></span></span>I agree all statements in <a
                    href="#" class="term-service">Terms of service</a></label>
              </div>
              <div class="form-group">
                <input type="submit" name="submit" id="submit" class="form-submit" value="Sign up"/>
              </div>
            </form>
            <p class="loginhere">
              Have already an account ? <a href="#" class="loginhere-link">Login here</a>
            </p>
          </div>
        </div>
      </section>

    </div>

  </div>
</template>

<script>
import $ from 'jquery';

export default {
  name: 'App',
  components: {},
  methods: {},
  mounted() {
    $(".toggle-password").click(function () {

      $(this).toggleClass("zmdi-eye zmdi-eye-off");
      var input = $($(this).attr("toggle"));
      if (input.attr("type") === "password") {
        input.attr("type", "text");
      } else {
        input.attr("type", "password");
      }
    });
  }
}
</script>

<style>
@import "assets/css/style.css";
@import "assets/fonts/material-icon/css/material-design-iconic-font.css";

@import 'assets/scss/common/extend.scss';
@import 'assets/scss/common/fonts.scss';
@import 'assets/scss/common/minxi.scss';
@import 'assets/scss/common/variables.scss';
@import 'assets/scss/common/global.scss';

@import 'assets/scss/layouts/main.scss';

@import 'assets/scss/layouts/responsive.scss';

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
