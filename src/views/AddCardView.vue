<template>
<section>
  <CardInfo :renderCard="newCard"/>
  <NewCardForm @updateCard="renderCard" @send="pushCard"/>
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
	},
	pushCard(createdCard){
		this.$emit('pushedCard', createdCard)
	}
}
}
</script>

<style>

</style>