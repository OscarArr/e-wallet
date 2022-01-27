<template>
	<div id="app">
		<HomeView v-if="view=='HomeView'" @changeView="view='AddCardView'" :cards="cardsArray" />
		<AddCardView v-if="view=='AddCardView'" @pushedCard="pushCreatedCard" :cards="cardsArray"/>
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
		cardNumber: "1234567890123456", 
		cardHolder: "Kent Aurén", 
		expireMonth: "3", 
		expireYear: "23", 
		CCV: '666'
		},
		{
		vendor: "blockchain", 
		cardNumber: "1234567890123156", 
		cardHolder: "Kent Aurén", 
		expireMonth: "3", 
		expireYear: "23", 
		CCV: '666'
		},
		{
		vendor: "evil", 
		cardNumber: "1337133713371337", 
		cardHolder: "OSCAR ARRHENIUS", 
		expireMonth: "13", 
		expireYear: "37", 
		CCV: '666'
		},
		{
		vendor: "ninja", 
		cardNumber: "1338133713371337", 
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
@import url('https://fonts.googleapis.com/css2?family=PT+Mono&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Source+Sans+Pro:wght@700&display=swap');

* {
	margin: 0;
	padding: 0;
	font-family: 'PT Mono', monospace;
}

h1, h2, h3, h4, h5, h6 {
	font-family: 'Source Sans Pro', sans-serif;
}

h1 {
	font-weight: bolder;
	font-size: 1.7rem;
}

h6 {
	color: darkgray;
}

#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	display: flex;
	flex-direction: column;
	align-items: center;
	min-width: 375px;
	max-width: 465px;
	// padding: 1rem;
	height: 100vh;
}
</style>
