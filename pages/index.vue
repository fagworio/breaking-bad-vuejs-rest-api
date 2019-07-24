<template>
  <div>
    <SearchFilter v-model="search" />

    <div class="section">
      <h1 class="title is-2 has-text-centered">Personagens</h1>
      <div class="row">
        <div class="buttons is-right spacer">
          <div class="filter">
            <p class="title is-6 no-padding">Filtre por:</p>
          </div>
          <a
            @click="filterKey = 'alive'"
            :class="[filterKey === 'alive' ? 'is-active' : 'is-outlined']"
            :disabled="search.length > 0 "
            class="button is-info"
          >Vivos</a>
          <a
            @click="filterKey = 'deads'"
            :class="[filterKey === 'deads' ? 'is-active' : 'is-outlined']"
            :disabled="search.length > 0 "
            class="button is-danger"
          >Mortos</a>
          <a
            @click="filterKey = 'all'"
            :class="[filterKey === 'all' ? 'is-active' : 'is-outlined']"
            :disabled="search.length > 0 "
            class="button is-primary"
          >Todos</a>
        </div>
      </div>

      <ListCharacters :characters="filteredList" />
      <nav class="pagination is-right" role="navigation" aria-label="pagination">
        <a
          class="pagination-previous"
          @click="previousPage"
          :disabled="this.count <= 10"
        >Página Anterior</a>
        <a class="pagination-next" @click="nextPage" :disabled="this.count >= 50">Próxima Página</a>
        <div class="pagination-list"></div>
      </nav>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import ListCharacters from "@/components/ListCharacters";
import SearchFilter from "@/components/SearchFilter";
export default {
  components: {
    ListCharacters,
    SearchFilter
  },
  data() {
    return {
      search: "",
      characters: [],
      filterKey: "all",
      count: 10,
      URL: "https://www.breakingbadapi.com/api/characters"
    };
  },
  methods: {
    async fetchData() {
      const res = await axios.get(this.URL + `?limit=10&offset=0`);
      this.characters = res.data;
    },
    async nextPage() {
      if (this.count < 50) {
        let pages = (this.count += 10);
        const res = await axios.get(this.URL + `?limit=10&offset=` + pages);
        this.characters = res.data;
      }
    },
    async previousPage() {
      if (this.count > 10) {
        let pages = (this.count -= 10);
        const res = await axios.get(this.URL + `?limit=10&offset=` + pages);
        this.characters = res.data;
      }
    },
    all() {
      return this.characters;
    },
    alives() {
      return this.characters.filter(actor => actor.status == "Alive");
    },
    deads() {
      return this.characters.filter(actor => actor.status == "Deceased");
    }
  },
  created() {
    this.fetchData();
  },
  computed: {
    filteredList() {
      if (this.search) {
        return this.characters.filter(actor => {
          return actor.name.toLowerCase().match(this.search.toLowerCase());
        });
      }
      if (this.filterKey === "alive") {
        return this.alives();
      }
      if (this.filterKey === "deads") {
        return this.deads();
      }
      if (this.filterKey === "all") {
        return this.characters.filter(actor => {
          return actor.name.toLowerCase().match(this.search.toLowerCase());
        });
      } else {
        return this.characters.filter(actor => {
          return actor.name.toLowerCase().match(this.search.toLowerCase());
        });
      }
    }
  }
};
</script>

<style scoped>
.spacer {
  padding-bottom: 10px;
}
.filter {
  margin-top: -10px;
  margin-right: 10px;
}
.button[disabled] {
  pointer-events: none;
}
</style>
