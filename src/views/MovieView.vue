<template>
	<div>
		<HeaderCont />
		<TitleCont />
		<FooterCont />
	</div>
</template>
<script>
import HeaderCont from '@/components/HeaderCont.vue';
import TitleCont from '@/components/TitleCont.vue';
import FooterCont from '@/components/FooterCont.vue';
export default {
	components: {
		HeaderCont,
		TitleCont,
		FooterCont,
	},
};
</script>
