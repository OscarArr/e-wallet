<template>
	<div id="app">
		<HomeView v-if="view=='HomeView'" @changeView="view='AddCardView'" :cards="cardsArray" />
		<AddCardView v-if="view=='AddCardView'" @pushedCard="pushCreatedCard"/>
	</div>
</template>

<script>
import AddCardView from './views/AddCardView.vue'
import HomeView from './views/HomeView.vue'

export default {
	name: 'App',
	components: {AddCardView, HomeView},
	data(){return{
		view: 'HomeView',
	cardsArray:[
		{
		vendor: "bitcoin", 
		cardNumber: "1234 5678 9012 3456", 
		cardHolder: "Kent Aurén", 
		expireMonth: "3", 
		expireYear: "23", 
		CCV: '666'
		},
		{
		vendor: "blockchain", 
		cardNumber: "1234 5678 9012 3156", 
		cardHolder: "Kent Aurén", 
		expireMonth: "3", 
		expireYear: "23", 
		CCV: '666'
		},
		{
		vendor: "evil", 
		cardNumber: "1337 1337 1337 1337", 
		cardHolder: "OSCAR ARRHENIUS", 
		expireMonth: "13", 
		expireYear: "37", 
		CCV: '666'
		},
		{
		vendor: "ninja", 
		cardNumber: "1338 1337 1337 1337", 
		cardHolder: "OSCAR ARRHENIUS", 
		expireMonth: "13", 
		expireYear: "37", 
		CCV: '666'
		}
	]
	}},
	methods: {
		pushCreatedCard(createdCard){
			this.cardsArray.push(createdCard)
			this.view = 'HomeView'
		}
	}
}
</script>

<style lang="scss">
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}
</style>
