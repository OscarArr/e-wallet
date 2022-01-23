<template>
<section>
  <CardInfo :renderCard="newCard"/>
  <NewCardForm @updateCard="renderCard"/>
</section>
</template>

<script>
import CardInfo from "../components/CardInfo.vue"
import NewCardForm from "../components/NewCardForm.vue"
export default {
components: {
	CardInfo, NewCardForm
},
data(){return{
	newCard:{}
}},
methods:{
	renderCard(cardInfo){
		this.newCard = cardInfo
	}
}
}
</script>

<style>

</style>