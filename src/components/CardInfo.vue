<template>
	<section v-if="card" @click="$emit('sendActiveCard', card)" :class="['card', classGenerator]">
		<div class="wifichip">
			<div class="wifi"></div>
			<div class="chip"></div>
		</div>
		<div class="logo"></div>
		<p v-if="card" class="card-number">{{ }}</p>
		<div class="cardholder-name">
			<p>CARDHOLDER NAME</p>
			<p v-if="card.cardHolder" class="cardholder">{{card.cardHolder.toUpperCase()}}</p>
		</div>
		<div class="valid-date">
			<p>VALID THRU</p>
			<div class="valid-MY">
				<p>{{card.expireMonth}}/{{card.expireYear}}</p>
			</div>
		</div>
	</section>
</template>

<script>
export default {
	updated(){
		// console.log(this.card)
		// this.dataLoaded = true
		// console.log(this.dataLoaded)
	},
	props:{
		renderCard: Object
	},
	data(){return{
		// dataLoaded: false
	}},
	computed:{
		card(){
			return this.renderCard
		},
		name(){
			return this.renderCard.cardHolder ? this.renderCard.cardHolder : 'Firstname Lastname'
		},
		classGenerator(){
			return this.card.vendor
		}
	}
}
</script>

<style scoped>
* {
	margin: 0;
}

.card {
	max-width: 21rem;
	width: 90vw;
	max-height: 13rem; 
	height: calc(90vw * 0.618);
	background-color: darkgray;
	border-radius: 0.5rem;
	box-shadow: 5px 5px 15px 5px rgba(0,0,0,0.5);
}

.card {
	padding: 1.5rem;
	display: grid;
	grid-template-areas: 
	"wifichip logo"
	"cardNumber cardNumber"
	"cardHolder validDate";
}

.card-number {
	grid-area: cardNumber;
}

.cardholder-name {
	grid-area: cardHolder;
}

.valid-date {
	grid-area: validDate;
}

.wifichip {
	grid-area: wifichip;
}

.logo{
	grid-area: logo;
	justify-self: flex-end;
}

.chip {
	/* background-image: url("../assets/chip.svg"); */
	background: url("../assets/chip.svg"), linear-gradient(90deg, rgba(179,176,174,1) 0%, rgba(223,207,189,1) 65%);
	border-radius: 8px;
	/* background-repeat: no-repeat; */
	height: 2.4rem;
}
.chip, .logo, .wifi {
	height: 2.4rem;
	width: 3rem;
	background-size: contain;
	background-repeat: no-repeat;
}

.valid-MY {
	display: flex;
	justify-content: center;
	align-items: center;
}


/* vendor card styles */

.empty .wifichip .wifi {
	background-image: url("../assets/wifi.svg");
	background-repeat: no-repeat;
}

.bitcoin {
	background: linear-gradient(248.04deg, rgba(255, 255, 255, 0.15) 0%, rgba(255, 255, 255, 0) 99.07%), #FFAE34;
}

.bitcoin .wifichip .wifi {
	background-image: url("../assets/wifi.svg");
	background-repeat: no-repeat;
}
.bitcoin .logo {
	background-image: url("../assets/bitcoin.svg");
	background-repeat: no-repeat;
}

.blockchain {
	background: linear-gradient(248.52deg, rgba(0, 0, 0, 0.15) 1.49%, rgba(0, 0, 0, 0) 100%), #8B58F9;
	color: white;
}

.blockchain .logo {
	background-image: url("../assets/blockchain.svg");
}

.blockchain .wifichip .wifi {
	background-image: url("../assets/wifi_white.svg");
	background-repeat: no-repeat;
}

.evil {
	background: linear-gradient(248.3deg, rgba(0, 0, 0, 0.16) 0%, rgba(0, 0, 0, 0) 100%), #F33355;
	color: white;
}

.evil .logo {
	background-image: url("../assets/evil.svg");
}

.evil .wifichip .wifi {
	background-image: url("../assets/wifi_white.svg");
	background-repeat: no-repeat;
}

.ninja {
	background: linear-gradient(248.3deg, rgba(255, 255, 255, 0.15) 0%, rgba(255, 255, 255, 0) 100%), #222222;
	color: white;
}

.ninja .logo {
	background-image: url("../assets/ninja.svg");
}

.ninja .wifichip .wifi {
	background-image: url("../assets/wifi_white.svg");
	background-repeat: no-repeat;
}

</style>