<template>
   
   <div id="app" class="container my-5">
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

</style>