<template>
    <div class="wrapper">
        <div class="movie-detail">
            <div class="card__info">
                <h2>{{movie.Title}}</h2>
                <p>{{ movie.Year }}</p>
            </div>
             <img :src="movie.Poster" alt="Movie Poster" class="featured-img">
            
            <div class="card__desc">
                <p>{{ movie.Plot }}</p>
            </div>
            
        </div>
    </div>
    
</template>

<script>
import { ref, onBeforeMount } from 'vue';
import { useRoute } from 'vue-router';
import env from '@/env.js';

export default {
    setup () {
        const movie = ref({});
        const route = useRoute();

        onBeforeMount(() => {
            fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
            .then(response => response.json())
            .then(data => {
                movie.value = data;
            })
        });

        return {
            movie
        }
    }
    
}
</script>

<style lang="scss">
    .movie-detail {
        padding: 16px;

        h2 {
            color: #fff;
            font-size: 28px;
            font-weight: 600;
            margin-bottom: 16px;
        }

        .featured-img {
            display: block;
            max-width: 200px;
            margin-bottom: 16px;
        }

        p {
            color: #fff;
            font-size: 18px;
            line-height: 1.4;
        }
    }

    @media (min-width: 479px) {
        .movie-detail {
            position: relative;
            padding-top: 0;

            .featured-img {
                width: 100%;
                max-width: 100%;
                height: 300px;
                object-fit: cover;
                position: relative;
                z-index: 0;
            }

            .card__info {
                position: absolute;
                left: 0;
                right: 0;
                top: 195px;
                background-color: rgba(0, 0, 0, 0.6);
                padding: 16px;
                margin: 0 16px;
                z-index: 1;
            }
        }
    }
</style>