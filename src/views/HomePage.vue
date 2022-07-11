<template>
	<div class="home">
		<div class="featured-card">
			<router-link :to="'/movie/'+topMovie.id">
				<img :src="firstPoster" :alt="topMovie.name" class="featured-img">
				<div class="detail">
					<h3>{{topMovie.name}}</h3>
					<p>{{topMovie.shortDescription}}</p>
				</div>
			</router-link>
		</div>

		<form @submit.prevent="searchMovies" class="search-box">
			<input type="text" placeholder="Enter the movie name" v-model="search">
			<button type="submit">Search movie</button>
		</form>

		<div class="founded" v-if="count > 0">Found <b>{{count}}</b> movies</div>

		<div class="movies-list">
			<div class="movie" v-for="movie in movies" :key="movie.id">

				<router-link :to="'/movie/'+movie.id" class="movie-link">
					<div class="movie-img">
						<img :src="movie.poster.url" :alt="movie.name">
						<div class="type">{{movie.type}}</div>
					</div>
					<div class="detail">
						<p class="year">{{movie.year}}</p>
						<h3>{{movie.name}}</h3>
					</div>
				</router-link>

			</div>
		</div>

	</div>
</template>

<script>

import axios from 'axios';

export default {
	data() {
		return {
			movies: [],
			isFound: false,
			search: '',
			topMovie: {},
			firstPoster: '',
			count: 0
		}
	},
	mounted() {
		axios.get(`https://api.kinopoisk.dev/movie/?token=ZQQ8GMN-TN54SGK-NB3MKEC-ZKB8V06&search=8-9&field=rating.kp&limit=1`)
			.then((response) => {
				this.topMovie = response.data.docs[0];
				this.firstPoster = this.topMovie.poster.url;
			})
	},
	methods: {
		searchMovies() {
			if(this.search != '') {
				axios.get(`https://api.kinopoisk.dev/movie/?token=ZQQ8GMN-TN54SGK-NB3MKEC-ZKB8V06&search=${this.search}&field=name&isStrict=false&limit=100`)
					.then((response) => {
						this.movies = response.data.docs;
						this.count = response.data.total;
						this.search = '';
						console.log(response.data);
				})
			}
		}
	}
}
</script>

<style lang="scss">
.home {
	.featured-card {
		position: relative;
		.featured-img {
			display: block;
			width: 100%;
			height: 300px;
			object-fit: cover;
			object-position: top;
			position: relative;
		}
		.detail {
			position: absolute;
			bottom:0;
			left: 0;
			right:0;
			background: rgba(0,0,0,0.6);
			padding: 16px;
			h3 {
				color:#fff;
				margin-bottom: 16px;
			}
			p {
				color:#fff;
			}
		}
	}
	.search-box {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 15px;

		input,
		button {
			display: block;
			border:none;
			outline: none;
			background: none;
			appearance: none;
		}
		input {
			width: 100%;
			color:#000;
			font-size: 20px;
			padding: 15px;
			background: #fff;
			border-radius: 4px;
			margin-bottom: 15px;
			transition: .4s;
			&:focus {
				box-shadow: 0 3px 6px rgba(255,255,255,0.4);
			}
		}
		button {
			width: 100%;
			cursor: pointer;
			background: #f60;
			padding: 16px;
			border-radius: 4px;
			font-size: 20px;
			color:#fff;
			text-transform: uppercase;
			transition: .4s;
			&:active {
				background: darken(#f60,20%);
			}
		}
	}
	.movies-list {
		display: flex;
		flex-wrap: wrap;
		margin: 0 8px;
		.movie {
			max-width: 50%;
			flex: 1 1 50%;
			padding: 15px 8px;
			.movie-link {
				display: flex;
				flex-direction: column;
				height: 100%;

				.movie-img {
					position: relative;
					display: block;
					img {
						display: block;
						width: 100%;
						min-height: 275px;
						object-fit: cover;
						object-position: top;
					}
					.type {
						position: absolute;
						padding: 8px 15px;
						background: #f60;
						color:#fff;
						bottom: 15px;
						left:0;
						text-transform: capitalize;
					}
				}
			}
		.detail {
			background: lighten(#f60, 10%);
			padding: 15px 8px;
			flex: 1 1 100%;
			border-radius: 0 0 8px 8px;

			.year {
				color:#fff;
				margin-bottom: 10px;
				font-size: 14px;
			}
			h3 {
				color: #fff;
				font-weight: bold;
				font-size: 18px;
			}
		}
		}
	}
	.founded {
		color:#fff;
		padding: 20px 15px;
		font-size: 20px;
		text-align: center;
	}
}

</style>