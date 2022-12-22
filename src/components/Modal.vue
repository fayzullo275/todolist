<template >
  <div class="modal">
    <div class="modal__card">
      <h2 class="modal__card-title" v-if="addOrChange">{{langWord.titlewindow[lang]}}</h2>
      <h2 class="modal__card-title" v-else>{{langWord.titlewindowedit[lang]}}</h2>
      
      <label class="modal__card-label">
        Title
        <input type="text" placeholder="Title" v-model="title" />
      </label>
      <label class="modal__card-label">
        Content
        <input type="text" placeholder="Content" v-model="content" />
      </label>
      <div class="modal__card-btns">
        <button @click="$emit('cancel', false)">{{langWord.closebtn[lang]}}</button>
        <button @click="addNote" v-if="addOrChange">{{langWord.addbtn[lang]}}</button>
        <button @click="saveNote" v-else>{{langWord.editwindowbtn[lang]}}</button>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    addOrChange: Boolean,
    saveChange: Object,
    langWord:Object,
    lang:String,
  },
  data() {
    return {
      title: "",
      content: "",
      time: "",
    };
  },
  methods: {
    addNote() {
      if (this.title != "" && this.content != "") {
        this.$emit("addNote", {
          title: this.title,
          content: this.content,
          time: new Date().toLocaleDateString(),
        });
      }
    },
    saveNote() {
      if (this.title != "" && this.content != "") {
        this.$emit("saveNote", {
          id: this.saveChange.id,
          title: this.title,
          content:this.content,
          time:new Date().toLocaleDateString()
        });
      }
    },
  },
  mounted() {
    if (!this.addOrChange) {
      this.title = this.saveChange.title;
      this.content = this.saveChange.content;
    }
  },
};
</script>
<style lang="">
</style>