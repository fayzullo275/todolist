<template >
  <div class="grid">
    <h2 class="grid__title">{{langWord.infobar[lang]}}</h2>
    <button class="grid__btn" @click="$emit('changeGrid',!gridOrList)">
      <img v-if="gridOrList" src="../assets/img/list.svg" alt="" />
      <img v-else src="../assets/img/grid.svg" alt="" />
      <span v-if="gridOrList">{{langWord.list[lang]}}</span>
      <span v-else>{{langWord.grid[lang]}}</span>
    </button>
  </div>
</template>
<script>
export default {
  props: {
    gridOrList: Boolean,
    langWord:Object,
    lang:String,
  },
 
};
</script>
<style lang="scss">
.grid {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 30px;
  &__title {
    font-weight: 400;
    font-size: 22px;
    line-height: 1.2;
    color: #323232;
  }
  &__btn {
    background: linear-gradient(
        0deg,
        rgba(103, 80, 164, 0.11),
        rgba(103, 80, 164, 0.11)
      ),
      #fffbfe;
    box-shadow: 0px 4px 8px 3px rgba(0, 0, 0, 0.15),
      0px 1px 3px rgba(0, 0, 0, 0.3);
    border-radius: 16px;
    width: 118px;
    height: 56px;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 15px;
    font-weight: 500;
    font-size: 14px;
    line-height: 20px;
    color: #6750a4;
  }
}
</style>