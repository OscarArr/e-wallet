<template>
<section>
	<h1>ADD A NEW BANK CARD</h1>
	<h6>NEW CARD</h6>
  <CardInfo :renderCard="newCard"/>
  <NewCardForm @updateCard="renderCard" @send="pushCard" :cards="cards"/>
</section>
</template>

<script>
import CardInfo from "../components/CardInfo.vue"
import NewCardForm from "../components/NewCardForm.vue"
export default {
props: {
	cards: Array
},
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

<style scoped>
section {
	display: flex;
	flex-direction: column;
	align-items: center;
}

h1 {
	width: 10rem;
}

h6 {
	margin: 1rem 0 0.2rem 0;
}


</style>