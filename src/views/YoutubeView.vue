<template>
	<div>
		<HeaderCont />
		<TitleCont name1="Youtube" name2="Reference" />
		<ContactCont />
		<FooterCont />
	</div>
</template>
<script>
import HeaderCont from '@/components/HeaderCont.vue';
import TitleCont from '@/components/TitleCont.vue';
import FooterCont from '@/components/FooterCont.vue';
import ContactCont from '@/components/ContactCont.vue';
export default {
	components: {
		HeaderCont,
		TitleCont,
		ContactCont,
		FooterCont,
	},
};
</script>
