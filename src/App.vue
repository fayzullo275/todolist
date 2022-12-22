<template>
  <div class="app">
    <Nav
      :lang="lang"
      :search="search"
      @searching="search = $event"
      @back="search = $event"
      @searchVal="searchInput = $event"
      @changeLang="lang = $event"
      :langWord="langWord"
    />
    <div class="container">
      <Grid 
       :gridOrList="gridOrList"
       @changeGrid="gridOrList = $event" 
       :langWord="langWord"
       :lang="lang"
       />
      <Cards 
      :grid="gridOrList" 
      :notes="notesFilter" 
      @changeNote="changeNote" 
      :langWord="langWord"
      :lang="lang"
      />
    </div>
    <AddBtn @changeModal="modal = $event" />
    <Modal
      v-if="modal"
      @addNote="addCard"
      @cancel="(modal = $event), (addOrChange = true)"
      :addOrChange="addOrChange"
      :saveChange="saveChange"
      @saveNote="saveNote"
      :langWord="langWord"
      :lang="lang"
    />
  </div>
</template>

<script>
import Modal from "./components/Modal";
import Grid from "./components/Grid.vue";
import Nav from "./components/Nav.vue";
import Cards from "./components/Cards.vue";
import AddBtn from "./components/AddBtn.vue";
import lang from "./lang";
export default {
  components: {
    Modal,
    Nav,
    Grid,
    Cards,
    AddBtn,
  },
  data() {
    return {
      lang: "uz",
      gridOrList: true,
      modal: false,
      notes: [],
      id: 1,
      addOrChange: true,
      saveChange: {},
      search: false,
      searchInput: "",
      langWord: {}
    };
  },
  methods: {
    addCard(cardObj) {
      (cardObj.id = this.id++), this.notes.push(cardObj);
      this.modal = false;
    },
    changeNote(cardId) {
      this.notes.forEach((card) => {
        if (cardId == card.id) {
          this.addOrChange = false;
          this.saveChange = {
            id: card.id,
            title: card.title,
            content: card.content,
          };
          this.modal = true;
        }
      });
    },
    saveNote(cardObj) {
      this.notes.forEach((card) => {
        if (card.id == cardObj.id) {
          card.title = cardObj.title;
          card.content = cardObj.content;
          card.time = cardObj.time;
          this.modal = false;
          this.addOrChange = true;
        }
      });
    },
  },
  computed: {
    notesFilter() {
      let array = this.notes;
      let search = this.searchInput;
      if (!this.search) return array;
      search = search.trim().toLowerCase();
      array = array.filter((note) => {
        if (note.title.toLowerCase().indexOf(search) != -1) return note;
      });
      return array;
    },
  },
  watch: {
    id() {
      localStorage.setItem("id", JSON.stringify(this.id));
    },
    notes: {
      handler(array) {
        localStorage.setItem("notes", JSON.stringify(array));
      },
      deep: true,
    },
  },
  created() {
    let localNotes = localStorage.getItem("notes");
    let localId = localStorage.getItem("id");
    this.langWord = lang
    if (localNotes) {
      this.notes = JSON.parse(localNotes);
    }
    if (localId) {
      this.id = JSON.parse(localId);
    }
  },
};
</script>


