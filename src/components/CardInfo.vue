<template>
	<section v-if="card" :class="['card', classGenerator]">
		<div class="wifichip">
			<div class="wifi"></div>
			<div class="chip"></div>
		</div>
		<div class="logo"></div>
		<p v-if="card" class="card-number">{{card.cardNumber}}</p>
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
	background-image: url("../assets/chip.svg");
	background-repeat: no-repeat;
}
.chip, .logo, .wifi {
	height: 3rem;
	width: 3rem;
	background-size: contain;
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
	background-color: linear-gradient(248.04deg, rgba(255, 255, 255, 0.15) 0%, rgba(255, 255, 255, 0) 99.07%), #FFAE34;
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
	background-color: linear-gradient(248.52deg, rgba(0, 0, 0, 0.15) 1.49%, rgba(0, 0, 0, 0) 100%), #8B58F9;
	background-image: url("../assets/blockchain.svg");
	background-position: right top;
	background-repeat: no-repeat;
}
.blockchain .wifichip .wifi {
	background-image: url("../assets/wifi_white.svg");
	background-repeat: no-repeat;
}

.evil {
	background-color: right top;
	background-image: url("../assets/evil.svg");
	background-repeat: no-repeat;
	background-position: linear-gradient(248.3deg, rgba(0, 0, 0, 0.16) 0%, rgba(0, 0, 0, 0) 100%), #F33355;
}

.evil .wifichip .wifi {
	background-image: url("../assets/wifi_white.svg");
	background-repeat: no-repeat;
}

.ninja {
	background-color: linear-gradient(248.3deg, rgba(255, 255, 255, 0.15) 0%, rgba(255, 255, 255, 0) 100%), #222222;
	background-image: url("../assets/ninja.svg");
	background-repeat: no-repeat;
	background-position: right top;
}

.ninja .wifichip .wifi {
	background-image: url("../assets/wifi_white.svg");
	background-repeat: no-repeat;
}

</style>