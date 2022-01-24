<template>
  <section>
      <h1>E-Wallet</h1>
      <article v-if="activeCard" class="active-card">
        <CardInfo :renderCard="activeCard"/>
      </article>
      <article class="card-stack">
          <CardInfo v-for="card in listOfCards" :key="card.cardNumber" :renderCard="card"/>
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
    },
    methods: {
        addCard(){
            this.$emit('changeView')
        }
    },
    data(){return{
        activeCard: null
    }}
}
</script>

<style>

</style>