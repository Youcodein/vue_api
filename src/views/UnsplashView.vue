<template>
	<div>
		<HeaderCont />
		<TitleCont name1="Unsplash" name2="Reference api" />
		<section class="cont__Refer">
			<div class="container">
				<div class="unsplash__inner">
					<div class="unsplash__slider"></div>
					<div class="unsplash__search"></div>
					<div class="unsplash__images">
						<ul>
							<li v-for="splash in splashes" :key="splash.id">
								<a href="#">
									<img :src="splash.urls.regular" :alt="splash.id" />
								</a>
							</li>
						</ul>
					</div>
				</div>
			</div>
		</section>
		<FooterCont />
		<ContactCont />
	</div>
</template>
<script>
import HeaderCont from '@/components/HeaderCont.vue';
import TitleCont from '@/components/TitleCont.vue';
import FooterCont from '@/components/FooterCont.vue';
import ContactCont from '@/components/ContactCont.vue';
import { ref } from 'vue';

export default {
	components: {
		HeaderCont,
		TitleCont,
		ContactCont,
		FooterCont,
	},
	setup() {
		const splashes = ref([]);
		const search = ref('landscape');

		// const SearchSplashes = () => {
		// 	fetch(
		// 		`https://api.unsplash.com/search/photos?client_id=rLzpIncf8xzBqXQBwEHmlns7US0iC_Se4GO-02oXIm4&query=${search.value}`,
		// 	)
		// 		.then(response => response.json())
		// 		.then(result => console.log(result))
		// 		.catch(error => console.log('error', error));
		// };
		// SearchSplashes();

		const RandomSplashes = () => {
			fetch(
				'https://api.unsplash.com/photos/random?client_id=rLzpIncf8xzBqXQBwEHmlns7US0iC_Se4GO-02oXIm4&count=20',
			)
				.then(response => response.json())
				.then(result => (splashes.value = result))
				.catch(error => console.log('error', error));
		};
		RandomSplashes();

		return {
			splashes,
			search,
			// SearchSplashes,
			RandomSplashes,
		};
	},
};
</script>

<style lang="scss">
.cont__Refer {
	.container {
		.unsplash__inner {
			.unsplash__slider {
			}
			.unsplash__search {
			}
			.unsplash__images {
				ul {
					display: flex;
					flex-wrap: wrap;
					justify-content: space-between;
					li {
						a {
							img {
								width: 300px;
							}
						}
					}
				}
			}
		}
	}
}
</style>
