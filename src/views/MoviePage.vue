<template>
	<div class="movie-detail">
		<h2>{{movie.name}}</h2>
		<p>{{movie.year}}</p>
		<img :src="movieImg" :alt="movie.name" class="featured-img">
		<p>{{movie.description}}</p>
	</div>
</template>

<script>

import axios from 'axios';
import { useRoute } from 'vue-router';

export default {
	data() {
		return {
			movie: {},
			movieImg: '',
			route: useRoute()
		}
	},
	beforeMount() {
		axios.get(`https://api.kinopoisk.dev/movie/?token=ZQQ8GMN-TN54SGK-NB3MKEC-ZKB8V06&search=${this.route.params.id}&field=id`)
			.then((response) => {
				this.movie = response.data;
				this.movieImg = this.movie.poster.url;
		})
	}
}
</script>

<style lang="scss">
	.movie-detail {
		padding: 16px;
		h2 {
			color:#fff;
			font-size: 28px;
			font-weight: bold;
			margin-bottom: 15px;
		}
		.featured-img {
			display: block;
			max-width: 200px;
			margin-bottom: 15px;
		}
		p {
			color:#fff;
			font-size: 18px;
			line-height: 1.4;
		}
	}
</style>