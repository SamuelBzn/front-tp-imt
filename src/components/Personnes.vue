<template>
  <div class="list row">
    <div class="col-md-6">
      <h4>Liste des personnes</h4>
      <ul class="list-group">
        <li class="list-group-item"
          :class="{ active: id == currentIndex }"
          v-for="(personne, id) in personnes"
          :key="id"
          @click="setActivePersonne(personne, id)"
        >
          {{ personne.surname }} {{ personne.name }}
        </li>
      </ul>
    </div>
    <div class="col-md-6">
      <div v-if="currentPersonne">
        <div>
          <label><strong>Nom:</strong></label> {{ currentPersonne.name }}
        </div>
        <div>
          <label><strong>Prénom:</strong></label> {{ currentPersonne.surname }}
        </div>
        <div>
          <label><strong>Téléphone:</strong></label> {{ currentPersonne.phone }}
        </div>
        <div>
          <label><strong>Ville:</strong></label> {{ currentPersonne.city }}
        </div>

        <router-link :to="'/personnes/' + currentPersonne.id" class="badge badge-warning">Modifier</router-link>
      </div>
      <div v-else>
        <br />
        <p>Cliquez sur une des personnes pour afficher les détails.</p>
      </div>
    </div>
  </div>
</template>

<script>
import PersonneDataService from "../services/PersonneDataService";

export default {
  name: "personnes",
  data() {
    return {
      personnes: [],
      currentPersonne: null,
      currentIndex: -1,
    };
  },
  methods: {
    getPersonnes() {
      PersonneDataService.getAll()
        .then(response => {
          this.personnes = response.data;
          console.log(response.data);
        })
        .catch(e => {
          console.log(e);
        });
    },

    setActivePersonne(personne, index) {
      this.currentPersonne = personne;
      this.currentIndex = personne ? index : -1;
    },
  },
  mounted() {
    this.getPersonnes();
  }
};
</script>

<style>
.list {
  text-align: left;
  max-width: 750px;
  margin: auto;
}
</style>
