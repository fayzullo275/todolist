<template>
  <div class="notes" :class="{setka:grid, list:!grid}" >
    <div class="card" v-for="(note,i) in notes" :key="i">
      <h2 class="card__title">{{note.title}}</h2>
      <p class="card__time">{{note.time}}</p>
      <p class="card__text">
        {{note.content}}
      </p>
      <div class="card__btn">
        <button class="card__btn-edit" @click="$emit('changeNote',note.id)">
          <img src="../assets/img/change.svg" alt="" />
         {{langWord.editbtn[lang]}}
        </button>
        <button class="card__btn-delete " @click="removeCard(note.id)">
          <img src="../assets/img/delete.svg" alt="" />
          {{langWord.deledit[lang]}}
        </button>
      </div>
    </div>
  </div>
</template>
<script>
export default {
    props:{
        grid:Boolean,
        notes:Array,
         langWord:Object,
    lang:String,
    },
    methods: {
      removeCard(cardId){
        this.notes.forEach((note,i) =>{
          if (note.id==cardId) {
            this.notes.splice(i,1);
          }
        })
      }
    },
};
</script>
<style lang="scss">
</style>