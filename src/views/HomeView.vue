<template>
  <section>
      <h1>E-Wallet</h1>
      <article v-if="activeCard" class="active-card">
		<h6>Active Card</h6>
        <CardInfo :renderCard="activeCard"/>
      </article>
      <article class="card-stack">
          <CardInfo v-for="card in cardsInStack" :key="card.cardNumber"
           @sendActiveCard="setActiveCard" :renderCard="card"/>
      </article>
      <button @click="addCard">ADD NEW CARD</button>
  </section>
</template>

<script>
import CardInfo from "../components/CardInfo.vue"
export default {
	mounted(){
		this.activeCard = this.cards[0]
	},
    components: {CardInfo},
    props: {
        cards: Array
    },
    computed: {
        cardsInStack(){
            return this.cards.filter(card => card != this.activeCard)
        }
    },
    methods: {
        addCard(){
            this.$emit('changeView')
        },
        setActiveCard(newActiveCard){
            this.activeCard = newActiveCard
        }
    },
    data(){return{
        activeCard: null
    }}
}
</script>

<style scoped>

	section {
		display: flex;
		flex-wrap: wrap;
		justify-content: center;

	}

	h1 {
		margin-top: 0.5rem;
		/* font-size: 1.3rem; */
	}

	h4 {
		font-size: 0.6rem;
	}

    .active-card {
		margin-top: 0.5rem;
	}
	
	.active-card section {
        margin-top: 0.3rem;
    }

    .card-stack{
        display: grid;
        grid-auto-rows: 1.5rem;
        height: 20rem;
        /* margin-bottom: 1rem; */
		/* max-width: 21rem; */
		/* width: 90vw; */
		box-shadow: 0;
    }

	button {
		margin-bottom: 1rem;
		padding: 1rem;
		width: 90%;
		align-self: flex-end;
	}

</style>