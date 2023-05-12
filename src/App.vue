<template>
  <div id="app">
    <Header />
    <div class="board">
      <div class="lane" v-for="(list, index) in cards" :key="index"
      v-on:dragenter="dragover(index)"
      >
        <h2 class="lane-title">{{list.title}}</h2>
        
          <Card draggable="true" class="card" v-for="card in list.cards" :key="card.id" 
          v-on:dragenter="dragstart(card.id)" 
          v-on:dragend="dragend()">
            {{card.text}}
          </Card>
      </div>
    </div>
  </div>
</template>

<script>

import Header from './components/Header';
import Card from './components/Card';
import initalCards from "./initalCards";


export default {
  name: 'App',
  components: {
    Header,
    Card
  },
  data: () => ({
    cards: [
      {title: 'Backlog', cards: initalCards.backlog},
      {title: 'Desenvolvimento', cards: initalCards.dev},
      {title: 'Testes', cards: initalCards.test},
      {title: 'Concluído', cards: []},
    ],
  }),
  methods: {
    dragstart(i){
      const cards = document.querySelectorAll('.card');

      cards[i - 1].classList.add('ativo');

    },
    dragover(index){
      const ativo = document.querySelector('.ativo');
      const lane = document.querySelectorAll('.lane');
      const laneCurrent = lane[index];
      laneCurrent.appendChild(ativo);
      
    },
    dragend() {
      const allActives = document.querySelectorAll('.ativo');

      allActives.forEach(item => {
        item.classList.remove('ativo')
      })
    }
  }
}
</script>

<style>
.board{
  display: flex;
  margin: 1.2rem .8rem;
  align-items: flex-start;
}

.lane{
  background: var(--color-grey);
  width: 23rem;
  border-radius: .8rem;
  box-shadow: 0 .1rem .2rem 0 rgba(33, 33, 33, 0.1);
  padding: 0 .7rem;
  margin: 0 .8rem
}

.lane-title{
  padding: .8rem .5rem;
  margin-bottom: .6rem;
}

.placeholder {
  background: rgba(33, 33, 33, .08);
  border-radius: .4rem;
  transform: scaleY(0.85);
  transform-origin: 0% 0%;
}

</style>
