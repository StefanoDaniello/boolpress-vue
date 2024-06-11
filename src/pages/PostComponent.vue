<template>
    <div v-if="post"> 
        <h1>{{ post.title }}</h1>
        <img :src="store.imgBasePath + post.image" :alt="post.title">
        <p>{{ post.content }}</p>
        <span>{{ post.category?.name }}</span> <br>
        <RouterLink :to="{ name: 'single-post', params: { 'slug': 'slirnsswww' } }">
            Leggi altro articolo</RouterLink>
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

</style>