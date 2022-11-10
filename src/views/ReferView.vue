<template>
	<div>
		<HeaderCont />
		<TitleCont name1="reference" name2="api" />
		<section className="cont__Refer">
			<div className="container">
				<div className="refer__inner">
					<h2>CSS</h2>
					<ul className="refer__list">
						<li v-for="refer in refers" :key="refer.title">
							<a href="#">
								<span class="num">{{ refer.num }}</span>
								<span class="name">{{ refer.name }}</span>
								<span class="desc">{{ refer.desc }}</span>
								<span class="descStar">{{ refer.descStar }}</span>
							</a>
						</li>
					</ul>
				</div>
			</div>
		</section>
		<ContactCont />
		<FooterCont />
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
		const refers = ref([]);

		const references = () => {
			fetch('https://youcodein.github.io/react_api/src/utils/reference.json')
				.then(response => response.json())
				// .then(result => console.log(result.cssRefer))
				.then(result => (refers.value = result.cssRefer))
				.catch(error => console.log('error', error));
		};
		references();

		return {
			refers,
			references,
		};
	},
};
</script>

<style lang="scss">
.refer__inner {
	padding-bottom: 200px;
	h2 {
		font-size: 40px;
		color: var(--black);
		margin-bottom: 50px;
	}
}

.refer__list {
	border: 1px solid var(--bg-light-border);

	li {
		border-bottom: 1px solid var(--bg-light-border);
		a {
			display: flex;
			align-items: center;
			width: 100%;
			color: var(--black);

			span {
				display: inline-block;
				padding: 15px 20px;
			}
			.num {
				flex: 1 1 5%;
				text-align: center;
				border-right: 1px solid var(--bg-light-border);
			}
			.name {
				flex: 1 1 20%;
				text-align: center;
				border-right: 1px solid var(--bg-light-border);
			}

			.desc {
				font-family: var(--font-kor2);
				flex: 1 1 50%;
				border-right: 1px solid var(--bg-light-border);
			}
			.descApply {
				font-family: var(--font-kor2);
				flex: 1 1 10%;
				text-align: center;
				border-right: 1px solid var(--bg-light-border);
			}
			.star {
				flex: 1 1 10%;
				text-align: center;
			}
		}
	}
}
</style>
