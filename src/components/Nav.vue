<template >
  <Transition name="nav" mode="out-in">
    <nav class="nav" v-if="!search">
      <Transition name="nav" mode="out-in">
        <button class="nav__lang" v-if="lang == 'ru'" @click="changeLang">
          Uz
          <img
            class="nav__lang-img"
            src="../assets/img/Uzbekistan-flag.webp"
            alt=""
          />
        </button>
        <button class="nav__lang" v-else @click="changeLang">
          Ru
          <img class="nav__lang-img" src="../assets/img/russia.png" alt="" />
        </button>
      </Transition>
      <div class="container">
        <h2 class="nav__title">{{langWord.appbartitle[lang]}}</h2>
      </div>
      <button class="nav__search" @click="$emit('searching', true)">
        <img src="../assets/img/search.svg" alt="" />
      </button>
    </nav>
    <nav class="nav" v-else>
      <button @click="back">
        <img src="@/assets/img/back.svg" alt="" />
      </button>
      <div class="container">
        <input
          class="nav__input"
          type="text"
          :placeholder="langWord.appbarseacrch[lang]"
          v-model="searchVal"
        />
      </div>
      <button class="nav__close">
        <img
          src="../assets/img/clear.svg"
          alt=""
          @click="this.searchVal = ''"
        />
      </button>
    </nav>
  </Transition>
</template>
<script>
export default {
  props: {
    lang: String,
    search: Boolean,
    langWord: Object,
  },
  data() {
    return {
      searchVal: "",
    };
  },
  methods: {
    back() {
      this.$emit("back", false);
      this.searchVal = "";
    },
    changeLang() {
      this.$emit("changeLang", this.lang == "uz" ? "ru" : "uz");
    },
  },
  watch: {
    searchVal(value) {
      this.$emit("searchVal", value);
    },
  },
};
</script>
<style lang="scss">
.nav-enter-active,
.nav-leave-active {
  transition: 0.5s;
}
.nav-enter-from,
.nav-leave-to {
  opacity: 0;
  transform: translateY(-100%);
}
</style>