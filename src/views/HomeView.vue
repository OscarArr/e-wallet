<template>
  <section>
      <h1>E-Wallet</h1>
      <article v-if="activeCard" class="active-card">
        <CardInfo :renderCard="activeCard"/>
      </article>
      <article class="card-stack">
          <CardInfo v-for="card in listOfCards" :key="card.cardNumber"
           @sendActiveCard="setActiveCard" :renderCard="card"/>
      </article>
      <button @click="addCard">ADD NEW CARD</button>
  </section>
</template>

<script>
import CardInfo from "../components/CardInfo.vue"
export default {
    components: {CardInfo},
    props: {
        cards: Array
    },
    computed: {
        listOfCards(){
            return this.cards
        }
        // activeCard(){
        //     return 
        // }
    },
    methods: {
        addCard(){
            this.$emit('changeView')
        },
        setActiveCard(newActiveCard){
            this.activeCard = newActiveCard
            // console.log(newActiveCard)
        }
    },
    data(){return{
        activeCard: null
    }}
}
</script>

<style scoped>
    .active-card {
        margin: 2rem;
    }

    .card-stack{
        display: grid;
        grid-auto-rows: 3rem;
        height: 25rem;
        margin-bottom: 1rem;
    }
/* 
    .card-stack .card {
        height: 3rem;
    } */

</style>