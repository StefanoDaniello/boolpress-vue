<template>
    <div class="container position-relative">
        <div class="pl container position-absolute d-flex justify-content-center align-items-center top-50 start-50 translate-middle" v-if="loading">
            <div class="gearbox">
            <div class="overlay"></div>
                <div class="gear one">
                    <div class="gear-inner">
                        <div class="bar"></div>
                        <div class="bar"></div>
                        <div class="bar"></div>
                    </div>
                </div>
                <div class="gear two">
                    <div class="gear-inner">
                        <div class="bar"></div>
                        <div class="bar"></div>
                        <div class="bar"></div>
                    </div>
                </div>
                <div class="gear three">
                    <div class="gear-inner">
                        <div class="bar"></div>
                        <div class="bar"></div>
                        <div class="bar"></div>
                    </div>
                </div>
                    <div class="gear four large">
                    <div class="gear-inner">
                        <div class="bar"></div>
                        <div class="bar"></div>
                        <div class="bar"></div>
                        <div class="bar"></div>
                        <div class="bar"></div>
                        <div class="bar"></div>
                    </div>
                </div>
            </div>
        </div>


    <h1>Contact Us</h1>
    <div v-if="success" class="alert alert-success text-start" role="alert">
        Messaggio inviato con successo!
    </div>

    
    <div class="row">
        <form @submit.prevent="sendForm()" class="col-12 text-start">
            <div class="mb-3">
                <input type="text" class="input border-0 border-bottom" :class="{ 'is-invalid': errors.name }"
                    placeholder="Name" v-model="name" required>
                <p v-for="(error, index) in errors.name" :key="`message-error-${index}`" class="invalid-feedback">
                    {{ error }}
                </p>
            </div>
            <div class="mb-3">
                <input type="email" class="input border-0 border-bottom" placeholder="Email" v-model="email"
                    :class="{ 'is-invalid': errors.address }" required>
                <p v-for="(error, index) in errors.address" :key="`message-error-${index}`" class="invalid-feedback">
                    {{ error }}
                </p>
            </div>
            <div class="mb-3">
                <textarea id="message" class="input border-0 border-bottom" cols="30" rows="10" placeholder="Message" v-model="message"
                    :class="{ 'is-invalid': errors.message }" required>{{ message }}</textarea>
                <p v-for="(error, index) in errors.message" :key="`message-error-${index}`" class="invalid-feedback">
                    {{ error }}
                </p>
            </div>
            <div class="d-flex">
                <button class="send">
                    <div class="svg-wrapper-1" type ="submit"
                        :disabled="loading" @click="sendAnimation()">
                        <div class="svg-wrapper">
                            <svg
                                xmlns="http://www.w3.org/2000/svg"
                                viewBox="0 0 24 24"
                                width="24"
                                height="24"
                            >
                                <path fill="none" d="M0 0h24v24H0z"></path>
                                <path
                                fill="currentColor"
                                d="M1.946 9.315c-.522-.174-.527-.455.01-.634l19.087-6.362c.529-.176.832.12.684.638l-5.454 19.086c-.15.529-.455.547-.679.045L12 14l6-8-8 6-8.054-2.685z"
                                ></path>
                            </svg>
                        </div>
                    </div>
                    <span>Send</span>
                </button>
                <!-- 
                <button class="btn btn-lg btn-primary text-white" type="submit" :disabled="loading">{{ loading ?
                'Sending...'
                : 'Send' }}
                </button> -->
                <!-- <button class="btn btn-lg btn-danger text-white mx-4" type="reset" @click="resetForm()"> 
                    Reset
                </button> -->
                <button class="btn-reset reset mx-3" @click="resetForm()">
                    <strong>Reset</strong>
                </button>

            </div>
           
        </form>
    </div>





    </div>
    
</template>

<script>
import { store } from '../store';
import axios from 'axios';
export default {
    name: 'ContactComponent',
    data() {
        return {
            store,
            name: '',
            email: '',
            message: '',
            errors: {},
            loading: false,
            success: false
        }
    },
    methods: {
        sendForm() {
            this.success = false;
            this.loading = true;
            this.errors = {};
            const data = {
                name: this.name,
                address: this.email,
                message: this.message
            }
            axios.post(this.store.apiBaseUrl + '/contacts', data).then((res) => {
                console.log(res.data.status);
                this.success = true;
                this.name = '';
                this.email = '';
                this.message = '';
            }).catch((error) => {
                console.log(error);
                this.errors = error.response.data.errors;
                // console.log(this.errors);
            }).finally(() => {
                this.loading = false;
            })
        },
        resetForm() {
            this.name = '';
            this.email = '';
            this.message = '';
            this.errors = {
                name: [],
                address: [],
                message: []
            };
        },
        sendAnimation() {
            const button = document.querySelector('.send');
            button.classList.add('animate');
            setTimeout(() => {
                button.classList.remove('animate');
            }, 3000);
        }
    }
}
</script>

<style lang="scss" scoped>

.reset {
  position: relative;
  margin: 0;
  padding: 17px 35px;
  outline: none;
  text-decoration: none;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  text-transform: uppercase;
  background-color: #fff;
  border: 1px solid rgba(255, 0, 0, 0.959);
  border-radius: 10px;
  color: #ff2222;
  font-weight: 400;
  font-family: inherit;
  z-index: 0;
  overflow: hidden;
  transition: all 0.3s cubic-bezier(0.02, 0.01, 0.47, 1);
}

.reset span {
  color: #bd2a2a;
  font-size: 14px;
  font-weight: 500;
  letter-spacing: 0.7px;
}

.reset:hover {
  animation: rotate624 0.7s ease-in-out both;
}

.reset:hover span {
  animation: storm1261 0.7s ease-in-out both;
  animation-delay: 0.06s;
}

@keyframes rotate624 {
  0% {
    transform: rotate(0deg) translate3d(0, 0, 0);
  }
  25% {
    transform: rotate(3deg) translate3d(0, 0, 0);
  }
  50% {
    transform: rotate(-3deg) translate3d(0, 0, 0);
  }
  75% {
    transform: rotate(1deg) translate3d(0, 0, 0);
  }
  100% {
    transform: rotate(0deg) translate3d(0, 0, 0);
  }
}

@keyframes storm1261 {
  0% {
    transform: translate3d(0, 0, 0) translateZ(0);
  }
  25% {
    transform: translate3d(4px, 0, 0) translateZ(0);
  }
  50% {
    transform: translate3d(-3px, 0, 0) translateZ(0);
  }
  75% {
    transform: translate3d(2px, 0, 0) translateZ(0);
  }
  100% {
    transform: translate3d(0, 0, 0) translateZ(0);
  }
}

.btn-reset {
  border: 1px solid;
  overflow: hidden;
  position: relative;
}

.btn-reset span {
  z-index: 20;
}

.btn-reset:after {
  background: #ef6338;
  content: "";
  height: 155px;
  left: -75px;
  opacity: 0.4;
  position: absolute;
  top: -50px;
  transform: rotate(35deg);
  transition: all 550ms cubic-bezier(0.19, 1, 0.22, 1);
  width: 50px;
  z-index: -10;
}

.btn-reset:hover:after {
  left: 120%;
  transition: all 550ms cubic-bezier(0.19, 1, 0.22, 1);
}


.send {
  font-family: inherit;
  font-size: 20px;
  background: rgb(7, 66, 245);
  color: white;
  padding: 0.7em 1em;
  padding-left: 0.9em;
  display: flex;
  align-items: center;
  border: none;
  border-radius: 16px;
  overflow: hidden;
  transition: all 0.2s;
  cursor: pointer;
}

.send span {
  display: block;
  margin-left: 0.3em;
  transition: all 0.3s ease-in-out;
}

.send svg {
  display: block;
  transform-origin: center center;
  transition: transform 0.3s ease-in-out;
}

.send:hover .svg-wrapper {
  animation: fly-1 0.6s ease-in-out infinite alternate;
}

.send:hover svg {
  transform: translateX(1.2em) rotate(45deg) scale(1.1);
}

.send:hover span {
  transform: translateX(5em);
}

.send:active {
  transform: scale(0.95);
}

@keyframes fly-1 {
  from {
    transform: translateY(0.1em);
  }

  to {
    transform: translateY(-0.1em);
  }
}


::placeholder {
    color: #ffffff96;
  }
.input {
  margin: 15px;
  background: none;
  border: none;
  outline: none;
  padding: 10px 20px;
  font-size: 16px;
  border-radius: 20px;
  width: 100%;
  box-shadow: inset 2px 5px 10px rgb(5, 5, 5);
  color: #fff;
 
}
@keyframes clockwise {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(360deg);
  }
}

@keyframes counter-clockwise {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(-360deg);
  }
}

.gearbox {
    z-index: 10;
  background: #111;
  height: 150px;
  width: 200px;
  position: relative;
  border: none;
  overflow: hidden;
  border-radius: 6px;
  box-shadow: 0px 0px 0px 1px rgba(255, 255, 255, 0.1);
}

.gearbox .overlay {
  border-radius: 6px;
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 10;
  box-shadow: inset 0px 0px 20px black;
  transition: background 0.2s;
}

.gearbox .overlay {
  background: transparent;
}

.gear {
  position: absolute;
  height: 60px;
  width: 60px;
  box-shadow: 0px -1px 0px 0px #888888, 0px 1px 0px 0px black;
  border-radius: 30px;
}

.gear.large {
  height: 120px;
  width: 120px;
  border-radius: 60px;
}

.gear.large:after {
  height: 96px;
  width: 96px;
  border-radius: 48px;
  margin-left: -48px;
  margin-top: -48px;
}

.gear.one {
  top: 12px;
  left: 10px;
}

.gear.two {
  top: 61px;
  left: 60px;
}

.gear.three {
  top: 110px;
  left: 10px;
}

.gear.four {
  top: 13px;
  left: 128px;
}

.gear:after {
  content: "";
  position: absolute;
  height: 36px;
  width: 36px;
  border-radius: 36px;
  background: #111;
  top: 50%;
  left: 50%;
  margin-left: -18px;
  margin-top: -18px;
  z-index: 3;
  box-shadow: 0px 0px 10px rgba(255, 255, 255, 0.1), inset 0px 0px 10px rgba(0, 0, 0, 0.1), inset 0px 2px 0px 0px #090909, inset 0px -1px 0px 0px #888888;
}

.gear-inner {
  position: relative;
  height: 100%;
  width: 100%;
  background: #555;
  border-radius: 30px;
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.large .gear-inner {
  border-radius: 60px;
}

.gear.one .gear-inner {
  animation: counter-clockwise 3s infinite linear;
}

.gear.two .gear-inner {
  animation: clockwise 3s infinite linear;
}

.gear.three .gear-inner {
  animation: counter-clockwise 3s infinite linear;
}

.gear.four .gear-inner {
  animation: counter-clockwise 6s infinite linear;
}

.gear-inner .bar {
  background: #555;
  height: 16px;
  width: 76px;
  position: absolute;
  left: 50%;
  margin-left: -38px;
  top: 50%;
  margin-top: -8px;
  border-radius: 2px;
  border-left: 1px solid rgba(255, 255, 255, 0.1);
  border-right: 1px solid rgba(255, 255, 255, 0.1);
}

.large .gear-inner .bar {
  margin-left: -68px;
  width: 136px;
}

.gear-inner .bar:nth-child(2) {
  transform: rotate(60deg);
}

.gear-inner .bar:nth-child(3) {
  transform: rotate(120deg);
}

.gear-inner .bar:nth-child(4) {
  transform: rotate(90deg);
}

.gear-inner .bar:nth-child(5) {
  transform: rotate(30deg);
}

.gear-inner .bar:nth-child(6) {
  transform: rotate(150deg);
}</style>