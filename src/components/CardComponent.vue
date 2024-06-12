<template>
    <div class="card mb-3">
        <div class="row g-0">
            <div class="col-12 col-md-4">
                <img :src="getImage" @error="setDefaultImage" class="img-fluid rounded-start" :alt="item.title">
            </div>
            <div class="col-md-8">
                <div class="card-body">
                    <h5 class="card-title ">{{ item.title }}</h5>
                    <p class="card-text" v-html="item.content"></p>
                    <p class="card-text"><small class="text-body-secondary">Last updated: {{ item.updated_at}}</small>
                    </p>
                    <span class="badge rounded-pill text-bg-warning me-3" >{{ item.category?.name }}</span>
                    <RouterLink :to="{ name: 'single-post', params: { 'slug': item.slug } }"  >
                        <button class="cta">
                        <span class="hover-underline-animation">  
                            Leggi
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
    </div>
</template>

<script>
import { store } from '../store';
export default {
    name: 'CardComponent',
    props: ['item'],
    data() {
        return {
            store
        }
    },
    computed: {
        getImage() {
            return this.item.image ? `${this.store.imgBasePath}${this.item.image}` : this.store.defaultImg;
        }
    },
    methods: {
        setDefaultImage(event) {
            event.target.src = this.store.defaultImg;
        }
    }
}
</script>

<style lang="scss" scoped>
.card-title {
    display: -webkit-box;
    -webkit-line-clamp: 1;     /* Numero massimo di righe */
    -webkit-box-orient: vertical;
    overflow: hidden;
    text-overflow: ellipsis;
    max-height: 2em;    
}
.card-text {
    display: -webkit-box;
    -webkit-line-clamp: 2;     /* Numero massimo di righe */
    -webkit-box-orient: vertical;
    overflow: hidden;
    text-overflow: ellipsis;
    max-height: 3em;    
}
.card{
    height: 250px;
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