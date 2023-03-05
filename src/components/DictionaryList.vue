<template>
  <div class="hello">
    <h1>Slovník {{ pocetSlov }}</h1>
    <div class="content">
      <form class="form--new-word" @submit.prevent="">
        <strong> Přidat slovo:</strong>
        <input
          type="text"
          class="input__term"
          v-model="newTitle"
          placeholder="Výraz"
        />
        <input
          type="text"
          class="input__term"
          v-model="newExpl"
          placeholder="Vysvětlení"
        />
        <button
          class="input__button--submit"
          type="submit"
          @click="addNewWords()"
        >
          Vložit
        </button>
      </form>
      <table class="slovnik">
        <draggable
          v-model="slovnik"
          group="people"
          @start="drag = true"
          @end="drag = true"
        >
          <tr v-for="(slovo, id) in slovnik" :key="slovo.id">
            <td>
              <div draggable="true" class="grabbable">#{{ id }}</div>
            </td>
            <td>
              <input type="text" class="input__term" v-model="slovo.title" />
            </td>
            <td>
              <input type="text" class="input__term" v-model="slovo.expl" />
            </td>
            <td>
              <button title="Vymazat" @click="vymaz(id)" class="del">x</button>
            </td>
          </tr>
        </draggable>
      </table>
    </div>
  </div>
</template>

<script>
// import randomWords from "random-words";
import draggable from "vuedraggable";

export default {
  name: "DictionaryList",
  components: {
    draggable
  },
  data() {
    return {
      newTitle: "",
      newExpl: "",
      slovnik: [
        {
          id: 0,
          title: "Adios",
          expl: "Say hi"
        },
        {
          id: 1,
          title: "Bulli",
          expl: "Bulifds "
        },
        {
          id: 2,
          title: "Cireladf",
          expl: "Somedir"
        },
        {
          id: 3,
          title: "Demoni",
          expl: "Dod Bulifds "
        },
        {
          id: 4,
          title: "Eviad",
          expl: "Korli"
        },
        { id: 5, title: "PsJcwQ", expl: "QFvTMX" },
        { id: 6, title: "ZVaTit", expl: "LyxrpI" },
        { id: 7, title: "VSXEGm", expl: "VaRFex" },
        { id: 8, title: "IGhsTv", expl: "FpwkHQ" },
        { id: 9, title: "NHahWJ", expl: "QkBTUN" },
        { id: 10, title: "PvJkTo", expl: "TPyNah" },
        { id: 11, title: "XBQrcJ", expl: "IRUeNZ" },
        { id: 12, title: "VhjNQV", expl: "EoSxFM" },
        { id: 13, title: "SakmiZ", expl: "KNklUA" },
        { id: 14, title: "JoXbPt", expl: "OoSZes" },
        { id: 15, title: "UWvhfx", expl: "Iqtcpm" },
        { id: 16, title: "NaKhAY", expl: "CAswqi" },
        { id: 17, title: "HCUTvq", expl: "EwuyBW" },
        { id: 18, title: "LaoYEs", expl: "YILlgU" },
        { id: 19, title: "RHShgT", expl: "MXGPUV" },
        { id: 20, title: "PoXYKz", expl: "NJKkYe" }
      ]
    };
  },
  methods: {
    vymaz(id) {
      this.slovnik.splice(id, 1);
    },
    addNewWords() {
      //let slovnikMaxId = this.slovnik.length ? Math.max(...this.slovnik.map(id => this.slovnik.id)) : 0;
      let slovnikMaxId = this.slovnik.length;
      this.slovnik.push({
        id: slovnikMaxId + 1,
        title: this.newTitle,
        expl: this.newExpl
      });
      this.newTitle = "";
      this.newExpl = "";
    }
  },
  computed: {
    pocetSlov() {
      if (this.slovnik.length > 40) {
        let celkemSlov = (this.slovnik.length * 2).toLocaleString("cs-CZ", {
          maximumFractionDigits: 0
        });
        return `${celkemSlov} slov`;
      } else return "";
    }
  },
  mounted() {
    const storageSlovnik = localStorage.getItem("slovnik");
    if (storageSlovnik) {
      {
        try {
          this.slovnik = JSON.parse(storageSlovnik);
        } catch (e) {
          console.error("chyba při localstorage čtení :>> ", e);
          localStorage.removeItem("slovnik");
        }
      }
    }
  },
  watch: {
    slovnik: {
      deep: true,
      handler() {
        localStorage.slovnik = JSON.stringify(this.slovnik);
      }
    }
  },
  async created() {
    const storageSlovnik = localStorage.getItem("slovnik");
    if (storageSlovnik == null) {
      // pokud ještě neexistuje local storage
      const response = await fetch(
        "https://run.mocky.io/v3/7c4bfaa2-de63-4a47-8b01-d566f44e23c9"
      );
      this.slovnik = await response.json();
    }
  }
};
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.content {
  display: flex;
  flex-direction: column;
  align-content: space-around;
  width: 900px;
  justify-content: center;
  margin: 0 auto;
  align-items: center;
}
.slovnik {
  padding: 2px;
  border-collapse: collapse;
}
.slovnik td {
  padding: 8px;
  border: 1px solid #eee;
  border-collapse: collapse;
}
.del {
  cursor: pointer;
}
.grabbable {
  cursor: move; /* fallback if grab cursor is unsupported */
  cursor: grab;
  cursor: -moz-grab;
  cursor: -webkit-grab;
}

/* (Optional) Apply a "closed-hand" cursor during drag operation. */
.grabbable:active {
  cursor: grabbing;
  cursor: -moz-grabbing;
  cursor: -webkit-grabbing;
}
.input__term {
  border: 1px solid #aaa;
  border-radius: 3px;
  padding: 5px;
}
.input__button--submit {
  cursor: pointer;
  padding: 4px;
  font-size: 1.3rem;
}
.form--new-word {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
  flex-direction: column;
  max-width: 230px;
  margin-bottom: 40px;
}
</style>
