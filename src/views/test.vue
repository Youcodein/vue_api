<template>
	<div>
		<HeaderCont />
		<TitleCont name1="movie" name2="reference api" />
		<section class="cont__refer">
			<div class="container">
				<div class="movie__inner">
					<div class="movie__slider">
						<swiper
							:effect="'coverflow'"
							:grabCursor="true"
							:centeredSlides="true"
							:slidesPerView="'auto'"
							:coverflowEffect="{
								rotate: 50,
								stretch: 0,
								depth: 100,
								modifier: 1,
								slideShadows: true,
							}"
							:pagination="true"
							:modules="modules"
							class="mySwiper"
						>
							<swiper-slide v-for="slider in sliders" :key="slider.id">
								<div class="item">
									<a href="#">
										<img
											:src="`https://image.tmdb.org/t/p/w500/${slider.poster_path}`"
											:alt="slider.title"
										/>
									</a>
								</div>
							</swiper-slide>
						</swiper>
					</div>
					<!-- movie__slider -->
					<div className="movie__search">
						<div className="container">
							<form @submit.prevent="SearchMovies()">
								<input
									type="search"
									id="search"
									placeholder="검색하세요!"
									v-model="search"
								/>
								<button type="submit">검색</button>
							</form>
						</div>
					</div>
					<!-- //movie__search -->
					<div class="movie__movies">
						<div class="container">
							<div class="movie__list">
								<ul>
									<li v-for="movie in movies" :key="movie.id">
										<a href="">
											<img
												:src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`"
												:alt="movie.title"
											/>
										</a>
									</li>
								</ul>
							</div>
						</div>
					</div>
					<!-- //movie__movies -->
				</div>
			</div>
		</section>
		<FooterCont />
		<ContactCont />
	</div>
</template>
<script>
import HeaderCont from '@/components/HeaderCont.vue';
import FooterCont from '@/components/FooterCont.vue';
import TitleCont from '@/components/TitleCont.vue';
import ContactCont from '@/components/ContactCont.vue';
import { ref } from 'vue';
import { Swiper, SwiperSlide } from 'swiper/vue';
// Import Swiper styles
import 'swiper/css';
import 'swiper/css/effect-coverflow';
import 'swiper/css/pagination';
// import "./style.css";
import { EffectCoverflow, Pagination } from 'swiper';
export default {
	components: {
		HeaderCont,
		FooterCont,
		TitleCont,
		ContactCont,
		Swiper,
		SwiperSlide,
	},
	setup() {
		const movies = ref([]);
		const sliders = ref([]);
		const search = ref('Disney');
		// async, await 데이터 다운이 늦을 수 있어서 비동기적으로 넣어주는 것임 리엑트에도!!
		const SearchMovies = async () => {
			await fetch(
				`https://api.themoviedb.org/3/search/movie?api_key=1fb50f08441e9552bb427c8e5f22096d&query=${search.value}`,
			)
				.then(response => response.json())
				.then(result => {
					console.log(result);
					movies.value = result.results;
					search.value = '';
				})
				.catch(error => console.log(error));
		};
		SearchMovies();
		const TopMovies = () => {
			fetch(
				`https://api.themoviedb.org/3/movie/popular?api_key=1fb50f08441e9552bb427c8e5f22096d`,
			)
				.then(response => response.json())
				.then(result => (sliders.value = result.results))
				.catch(error => console.log(error));
		};
		TopMovies();
		return {
			movies,
			sliders,
			search,
			SearchMovies,
			modules: [EffectCoverflow, Pagination],
		};
	},
};
</script>
<style lang="scss">
.movie__inner {
	ul {
		display: flex;
		justify-content: space-between;
		flex-wrap: wrap;
		li {
			width: 18%;
			position: relative;
			em {
				display: block;
				height: 80px;
				margin-bottom: 60px;
				font-family: var(--font-kor2);
			}
			.title {
				padding: 5px 0;
				display: inline-block;
			}
			.star {
				background: #fff;
				color: #000;
				border-radius: 100px;
				position: absolute;
				right: 10px;
				top: 10px;
				width: 40px;
				height: 30px;
				text-align: center;
				line-height: 30px;
				font-weight: 800;
			}
		}
	}
	a {
		color: var(--black);
	}
}
.movie__search {
	margin-bottom: 100px;
	.container {
		position: relative;
	}
	h2 {
		color: var(--black);
		font-size: 40px;
		text-indent: -9999px;
		height: 0;
	}
	input {
		background: #fff;
		border: 2px solid var(--white);
		border-radius: 50px;
		color: var(--black);
		width: 100%;
		padding: 14px 30px;
		font-family: var(--font-kor2);
	}
	button {
		position: absolute;
		right: 6px;
		top: 7px;
		width: 40px;
		height: 40px;
		border-radius: 50%;
		border: 0;
		font-family: var(--font-kor2);
		cursor: pointer;
		z-index: 1000;
	}
}
.Movie__slider {
	height: 800px;
	.swiper {
		width: 100%;
		padding-top: 50px;
		padding-bottom: 50px;
	}
	.swiper-slide {
		background-position: center;
		background-size: cover;
		width: 300px;
		height: 300px;
	}
	.swiper-slide img {
		display: block;
		width: 100%;
	}
}
.Movielist {
	position: relative;
	transition: all 0.4s;
	&:hover {
		transform: scale(1.07);
	}
	.rank {
		font-size: 80px;
		position: absolute;
		top: -50px;
		left: -10px;
		text-shadow: 4px 4px 2px rgba(255, 255, 255, 0.4);
		z-index: 10000;
	}
	.MovieImg {
		width: 300px;
	}
	.Moviestar {
		background: #fff;
		color: #000;
		border-radius: 100px;
		position: absolute;
		right: -230px;
		top: -35px;
		width: 40px;
		height: 25px;
		text-align: center;
		line-height: 25px;
		font-weight: 800;
	}
}
</style>
