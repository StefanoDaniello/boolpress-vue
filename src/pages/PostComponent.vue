<template>
   
   <div id="app" class="container my-5">
    <RouterLink :to="{ name: 'posts'}" >
        <button class="back-button m-5">
            <div class="back-button-box">
            <span class="back-button-elem">
                <svg viewBox="0 0 46 40" xmlns="http://www.w3.org/2000/svg">
                <path
                    d="M46 20.038c0-.7-.3-1.5-.8-2.1l-16-17c-1.1-1-3.2-1.4-4.4-.3-1.2 1.1-1.2 3.3 0 4.4l11.3 11.9H3c-1.7 0-3 1.3-3 3s1.3 3 3 3h33.1l-11.3 11.9c-1 1-1.2 3.3 0 4.4 1.2 1.1 3.3.8 4.4-.3l16-17c.5-.5.8-1.1.8-1.9z"
                ></path>
                </svg>
            </span>
            <span class="back-button-elem ">
                <svg viewBox="0 0 46 40">
                <path
                    d="M46 20.038c0-.7-.3-1.5-.8-2.1l-16-17c-1.1-1-3.2-1.4-4.4-.3-1.2 1.1-1.2 3.3 0 4.4l11.3 11.9H3c-1.7 0-3 1.3-3 3s1.3 3 3 3h33.1l-11.3 11.9c-1 1-1.2 3.3 0 4.4 1.2 1.1 3.3.8 4.4-.3l16-17c.5-.5.8-1.1.8-1.9z"
                ></path>
                </svg>
            </span>
            </div>
        </button>
    </RouterLink>
  

        <div v-if="post" class="card">
            <img :src="store.imgBasePath + post.image" class="card-img-top" :alt="post.title">
            <div class="card-body">
                <h5 class="card-title">{{ post.title }}</h5>
                <p class="card-text">{{ post.content }}</p>
                <span class="badge badge-primary">{{ post.category?.name }}</span> <br>
                <RouterLink :to="{ name: 'single-post', params: { 'slug': 'slirnsswww' } }" class="btn ">
                    <button class="cta">
                        <span class="hover-underline-animation">  
                            Altro articolo
                        </span>
                        <svg
                            id="arrow-horizontal"
                            xmlns="http://www.w3.org/2000/svg"
                            width="30"
                            height="10"
                            viewBox="0 0 46 16"
                        >
                            <path
                            id="Path_10"
                            data-name="Path 10"
                            d="M8,0,6.545,1.455l5.506,5.506H-30V9.039H12.052L6.545,14.545,8,16l8-8Z"
                            transform="translate(30)"
                            ></path>
                        </svg>
                    </button>
                </RouterLink> 
                
            </div>
        </div>
    </div>
</template>

<script>
import { store } from '../store';
import axios from 'axios';
export default {
    name: "PostComponent",
    
    data() {
        return {
            store,
            post: null,
        }
    },
    methods: {
        getPost() {
            axios.get(`${this.store.apiBaseUrl}/posts/${this.$route.params.slug}`).then((res) => {
                console.log(res.data.results);
                this.post = res.data.results;
            }).catch((err) => {
                console.log(err);
                // console.log(err.response.data);
                // Il push corrisponde al redirect  
                this.$router.push({ name: 'not-found' });
            }).finally(() => {
                // console.log('finally');
            })
        },
    },
    mounted() {
        this.getPost();
    },
    created() {
        this.$watch(
            () => this.$route.params,
            (toParams, previousParams) => {
                // react to route changes...
                this.getPost();
            }
        )
    }
}
</script>

<style lang="scss" scoped>
    .card {
        max-width: 620px;
        margin: 0 auto;
    }
    .cta {
  border: none;
  background: none;
  cursor: pointer;
}

.cta span {
  padding-bottom: 7px;
  letter-spacing: 4px;
  font-size: 14px;
  padding-right: 15px;
  text-transform: uppercase;
}

.cta svg {
  transform: translateX(-8px);
  transition: all 0.3s ease;
}

.cta:hover svg {
  transform: translateX(0);
}

.cta:active svg {
  transform: scale(0.9);
}

.hover-underline-animation {
  position: relative;
  color: black;
  padding-bottom: 20px;
}

.hover-underline-animation:after {
  content: "";
  position: absolute;
  width: 100%;
  transform: scaleX(0);
  height: 2px;
  bottom: 0;
  left: 0;
  background-color: #000000;
  transform-origin: bottom right;
  transition: transform 0.25s ease-out;
}

.cta:hover .hover-underline-animation:after {
  transform: scaleX(1);
  transform-origin: bottom left;
}


//back-button
    .back-button {
    display: block;
    position: relative;
    width: 56px;
    height: 56px;
    margin: 0;
    overflow: hidden;
    outline: none;
    background-color: transparent;
    cursor: pointer;
    border: 0;
    }

    .back-button:before,
    .back-button:after {
    content: "";
    position: absolute;
    border-radius: 50%;
    inset: 7px;
    }

    .back-button:before {
    border: 4px solid #f0eeef;
    transition: opacity 0.4s cubic-bezier(0.77, 0, 0.175, 1) 80ms,
        transform 0.5s cubic-bezier(0.455, 0.03, 0.515, 0.955) 80ms;
    }

    .back-button:after {
    border: 4px solid #77e0c1;
    transform: scale(1.3);
    transition: opacity 0.4s cubic-bezier(0.165, 0.84, 0.44, 1),
        transform 0.5s cubic-bezier(0.25, 0.46, 0.45, 0.94);
    opacity: 0;
    }

    .back-button:hover:before,
    .back-button:focus:before {
    opacity: 0;
    transform: scale(0.7);
    transition: opacity 0.4s cubic-bezier(0.165, 0.84, 0.44, 1),
        transform 0.5s cubic-bezier(0.25, 0.46, 0.45, 0.94);
    }

    .back-button:hover:after,
    .back-button:focus:after {
    opacity: 1;
    transform: scale(1);
    transition: opacity 0.4s cubic-bezier(0.77, 0, 0.175, 1) 80ms,
        transform 0.5s cubic-bezier(0.455, 0.03, 0.515, 0.955) 80ms;
    }

    .back-button-box {
    display: flex;
    position: absolute;
    top: 0;
    left: 0;
    }

    .back-button-elem {
    display: block;
    width: 20px;
    height: 20px;
    margin: 21px 18px 0 18px;
    transform: rotate(180deg);
    fill: #f0eeef;
    }

    .back-button:hover .back-button-box,
    .back-button:focus .back-button-box {
    transition: 0.4s;
    transform: translateX(-56px);
    }


</style>