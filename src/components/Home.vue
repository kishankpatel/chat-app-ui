<template>
  <div class="authentication-wrapper authentication-3" style="min-height: 88vh">
    <div class="authentication-inner">
      <!-- Side container -->
      <!-- Do not display the container on extra small, small and medium screens -->
      <div
        class="d-none d-lg-flex col-lg-8 align-items-center ui-bg-cover ui-bg-overlay-container p-5"
        :style="`background-image: url('${baseUrl}img/bg/21.jpg')`"
      >
        <div class="ui-bg-overlay bg-dark opacity-50"></div>

        <!-- Text -->
        <div class="w-100 text-white px-5">
          <h1 class="display-2 font-weight-bolder mb-4">
            JOIN OUR
            <br />COMMUNITY
          </h1>
          <div
            class="text-large font-weight-light"
          >Francium's core purpose is to create technology solutions for progressive and forward-thinking organizations to empower their ascendancy and to magnify their impact. We envision being the front-runners when it comes to technology and a resource centre for mid-sized organizations to full-fledged enterprises.</div>
        </div>
        <!-- /.Text -->
      </div>
      <!-- / Side container -->

      <!-- Form container -->
      <div class="d-flex col-lg-4 align-items-center bg-white p-5">
        <!-- Inner container -->
        <!-- Have to add `.d-flex` to control width via `.col-*` classes -->
        <div class="d-flex col-sm-7 col-md-5 col-lg-12 px-0 px-xl-4 mx-auto">
          <div class="w-100">
            <!-- Logo -->
            <div class="d-flex justify-content-center align-items-center">
              <div class="ui-w-60">
                <div class="w-100 position-relative" style="padding-bottom: 54%">
                  <!-- <b-img :src="`${baseUrl}img/logo.png`" width="100"></b-img> -->
                  <svg
                    class="w-100 h-100 position-absolute"
                    viewBox="0 0 148 80"
                    xmlns="http://www.w3.org/2000/svg"
                    xmlns:xlink="http://www.w3.org/1999/xlink"
                  >
                    <defs>
                      <linearGradient
                        id="a"
                        x1="46.49"
                        x2="62.46"
                        y1="53.39"
                        y2="48.2"
                        gradientUnits="userSpaceOnUse"
                      >
                        <stop stop-opacity=".25" offset="0" />
                        <stop stop-opacity=".1" offset=".3" />
                        <stop stop-opacity="0" offset=".9" />
                      </linearGradient>
                      <linearGradient
                        id="e"
                        x1="76.9"
                        x2="92.64"
                        y1="26.38"
                        y2="31.49"
                        xlink:href="#a"
                      />
                      <linearGradient
                        id="d"
                        x1="107.12"
                        x2="122.74"
                        y1="53.41"
                        y2="48.33"
                        xlink:href="#a"
                      />
                    </defs>
                    <path
                      class="fill-primary"
                      transform="translate(-.1)"
                      d="M121.36,0,104.42,45.08,88.71,3.28A5.09,5.09,0,0,0,83.93,0H64.27A5.09,5.09,0,0,0,59.5,3.28L43.79,45.08,26.85,0H.1L29.43,76.74A5.09,5.09,0,0,0,34.19,80H53.39a5.09,5.09,0,0,0,4.77-3.26L74.1,35l16,41.74A5.09,5.09,0,0,0,94.82,80h18.95a5.09,5.09,0,0,0,4.76-3.24L148.1,0Z"
                    />
                    <path
                      transform="translate(-.1)"
                      d="M52.19,22.73l-8.4,22.35L56.51,78.94a5,5,0,0,0,1.64-2.19l7.34-19.2Z"
                      fill="url(#a)"
                    />
                    <path
                      transform="translate(-.1)"
                      d="M95.73,22l-7-18.69a5,5,0,0,0-1.64-2.21L74.1,35l8.33,21.79Z"
                      fill="url(#e)"
                    />
                    <path
                      transform="translate(-.1)"
                      d="M112.73,23l-8.31,22.12,12.66,33.7a5,5,0,0,0,1.45-2l7.3-18.93Z"
                      fill="url(#d)"
                    />
                  </svg>
                </div>
              </div>
            </div>
            <!-- / Logo -->

            <h4 class="text-center text-lighter font-weight-normal mt-5 mb-0">Login to Your Account</h4>

            <!-- Form -->
            <b-form class="my-5" @submit.prevent="submitForm()">
              <b-form-group label="Username">
                <b-input v-model="credentials.username" />
                <div class="text-danger small" v-show="showError">
                  Username is required.
                </div>
              </b-form-group>
              <!-- <b-form-group>
                <div slot="label" class="d-flex justify-content-between align-items-end">
                  <div>Password</div>
                  <a href="javascript:void(0)" class="d-block small">Forgot password?</a>
                </div>
                <b-input type="password" v-model="credentials.password" />
              </b-form-group>-->
              <div class="d-flex justify-content-between align-items-center m-0">
                <!-- <b-check v-model="credentials.rememberMe" class="m-0">Remember me</b-check> -->
                <b-btn type="submit" variant="primary">Sign In</b-btn>
              </div>
            </b-form>
            <!-- / Form -->

            <!-- <div class="text-center text-muted">
              Don't have an account yet?
              <a href="javascript:void(0)">Sign Up</a>
            </div>-->
          </div>
        </div>
      </div>
      <!-- / Form container -->
    </div>
  </div>
</template>

<!-- Page -->
<style src="@/vendor/styles/pages/authentication.scss" lang="scss"></style>

<script>
import utility from "../mixins/utility"
export default {
  name: 'pages-authentication-login-v3',
  metaInfo: {
    title: 'Login'
  },
  data: () => ({
    credentials: {
      username: ''
      // password: '',
      // rememberMe: false,
    },
    webSocket: null,
    showError: false
  }),
  mixins: [utility],
  methods: {
    submitForm() {
      if (!this.credentials.username.trim()) {
        this.showError = true
        return false
      }
      var self = this
      var socket = new WebSocket("ws://localhost:4040/register")
      socket.onopen = function(e) {

        socket.send(
          JSON.stringify({
            UserName: self.credentials.username
          }
        ))

        socket.onmessage = function(e) {
          self.handleSocketResponse(JSON.parse(e.data))
        };

        socket.onclose = function(e) {
          // self.closingSocket(e)
        }

      }
    }
  }
}
</script>
