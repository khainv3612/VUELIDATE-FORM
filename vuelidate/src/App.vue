<template>
  <div id="app">
    <div class="main">
      <section class="signup">
        <div class="container">
          <div class="signup-content">
            <form @submit.prevent="handleSubmit" id="signup-form" class="signup-form">
              <h2 class="form-title">Create account</h2>
              <div class="form-group">
                <input type="text" class="form-input" v-model.trim="$v.name.$model" id="name"
                       placeholder="Your Name"/>
                <div class="error" v-if="submitted && !$v.name.required">Name is required</div>
                <div
                    class="error"
                    v-if="submitted && !$v.name.minLength"
                >Name must have at least {{ $v.name.$params.minLength.min }} letters.
                </div>
                <div
                    class="error"
                    v-if="submitted && !$v.name.maxLength"
                >Name must have at most {{ $v.name.$params.maxLength.max }} letters.
                </div>
              </div>
              <div class="form-group">
                <input type="email" class="form-input" name="email" id="email" placeholder="Your Email"
                       v-model.trim="email"/>
                <div class="error" v-if="submitted && !$v.email.required">Email is required</div>
                <div class="error" v-if="!$v.email.email">Email must be valid</div>
              </div>
              <div class="form-group">
                <input type="text" class="form-input" name="password" id="password" placeholder="Password"
                       v-model="password"/>
                <span toggle="#password" class="zmdi zmdi-eye field-icon toggle-password"></span>
                <div class="error" v-if="submitted && !$v.password.valid">Password between 8 to 15 characters, at least
                  one lowercase letter, one uppercase letter, one numeric digit, and one special character
                </div>
              </div>
              <div class="form-group">
                <input type="password" class="form-input" name="re_password" id="re_password" v-model="repass"
                       placeholder="Repeat your password"/>
                <div class="error" v-if="submitted && !$v.repass.sameAsPassword">Pass not match</div>
              </div>
              <div class="form-group">
                <input type="checkbox" name="agree-term" id="agree-term" class="agree-term" v-model="isAgree"/>
                <label for="agree-term" class="label-agree-term"><span><span></span></span>I agree all statements in <a
                    href="#" class="term-service">Terms of service</a></label>
                <div class="error" v-if="submitted && !isAgree">Please accept term</div>
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
import {validationMixin} from "vuelidate";
import {required, email, minLength, maxLength, sameAs} from "vuelidate/lib/validators";


export default {
  name: 'App',
  components: {},
  data() {
    return {
      name: "",
      email: "",
      password: "",
      repass: "",
      isAgree: false,
      submitted: false
    }
  },
  mixins: [validationMixin],
  validations: {
    name: {
      required,
      minLength: minLength(6),
      maxLength: maxLength(20),
    },
    email: {
      required,
      email
    },
    password: {
      required,
      valid: function (value) {
        return /^(?=.*\d)(?=.*[a-z])(?=.*[A-Z])(?=.*[^a-zA-Z0-9])(?!.*\s).{8,15}$/.test(value);
      }
    },
    repass: {required, sameAsPassword: sameAs('password')}
  },
  methods: {
    handleSubmit() {
      this.submitted = true;
      if (!this.isAgree)
        return;
      this.$v.$touch();
      if (this.$v.$invalid) {
        // alert("Please complete all field correctly");
        return
      }
    }
  },
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

.error {
  color: red;
  text-align: left;
}
</style>
