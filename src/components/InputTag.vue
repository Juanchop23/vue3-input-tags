<script>
export default {
  //Cada vez que haya un cambio, se va a devolver la lista de etiquetas
  props: ["onTagsChange"],
  data() {
    return {
      currentValue: "",
      tags: [],
    };
  },

  methods: {
    handleKeyDown(e) {
      //Al presionar una tecla, se borra una etiqueta
      if (e.key === "Backspace" && this.currentValue === "") {
        this.tags.pop();
        this.onTagsChange(this.tags);
      }
    },
    handleSubmit() {
      //Almacenar un valor
      if (this.currentValue !== "") {
        //Filtrar para que no agregue elementos ya existentes
        const exist = this.tags.some((item) => item == this.currentValue);
        if (!exist) {
          this.tags.push(this.currentValue);
          this.currentValue = "";
          this.onTagsChange(this.tags);
        }
      }
    },
    deleteTag(tag) {
      this.tags = this.tags.filter((item) => item !== tag);
      this.onTagsChange(this.tags);

      console.log(this.tags);
    },
  },
};
</script>

<template>
  <div class="inputTag">
    <div class="tags">
      <div class="tag" v-for="(tag, index) in tags" :key="index">
        {{ tag }} <button @click="deleteTag(tag)">X</button>
      </div>
    </div>
    <!-- Es mejor hacerlo con un formulario para no estar mapeando eventos del teclado -->
    <form @submit.prevent="handleSubmit">
      <input
        type="text"
        class="input"
        v-model="currentValue"
        @keydown="handleKeyDown"
      />
    </form>
  </div>
</template>

<style scoped>
.inputTag {
  display: inline-flex;
  border: solid 1px #000;
  border-radius: 3px;
  height: 43px;
}

.tags {
  display: flex;
  gap: 3px;
  padding: 5px;
}

.tags .tag {
  display: flex;
  padding: 5px;
  border: solid 1px #ccc;
  gap: 5px;
  align-items: center;
  border-radius: 3px;
}

.inputTag form {
  display: flex-inline;
}

.inputTag .input {
  border: none;
  outline: none;
  padding: 0 5 px;
}

.inputTag button {
  background-color: transparent;
  border: none;
  border-radius: 3px;
  cursor: pointer;
}

.inputTag button:hover {
  background-color: #eee;
}
</style>
