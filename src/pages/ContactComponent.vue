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
                <button class="btn btn-lg btn-primary text-white" type="submit" :disabled="loading">{{ loading ?
                'Sending...'
                : 'Send' }}
                </button>
                <button class="btn btn-lg btn-danger text-white mx-4" type="reset" @click="resetForm()"> 
                    Reset
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
        }
    }
}
</script>

<style lang="scss" scoped>

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