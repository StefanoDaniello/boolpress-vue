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
                    <span class="badge rounded-pill text-bg-warning me-3">{{ item.category?.name }}</span>
                    <RouterLink :to="{ name: 'single-post', params: { 'slug': item.slug } }" class="btn btn-success">
                        Leggi articolo</RouterLink>
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

</style>