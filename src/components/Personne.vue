<template>
  <div v-if="currentPersonne" class="edit-form">
    <h4>Personne</h4>
    <form>
      <div class="form-group">
        <label for="id">ID</label>
        <input type="text" readonly class="form-control" id="id"
          v-model="currentPersonne.id"
        />
      </div>

      <div class="form-group">
        <label for="name">Nom</label>
        <input type="text" class="form-control" id="name"
          v-model="currentPersonne.name"
        />
      </div>

      <div class="form-group">
        <label for="surname">Prénom</label>
        <input type="text" class="form-control" id="surname"
          v-model="currentPersonne.surname"
        />
      </div>

      <div class="form-group">
        <label for="phone">Téléphone</label>
        <input type="text" class="form-control" id="phone"
          v-model="currentPersonne.phone"
        />
      </div>

      <div class="form-group">
        <label for="city">Ville</label>
        <input type="text" class="form-control" id="city"
          v-model="currentPersonne.city"
        />
      </div>
    </form>

    <button class="badge badge-danger mr-2"
      @click="deletePersonne"
    >
      Supprimer
    </button>

    <button type="submit" class="badge badge-success"
      @click="updatePersonne"
    >
      Modifier
    </button>
    <p>{{ message }}</p>
  </div>
</template>

<script>
import PersonneDataService from "../services/PersonneDataService";

export default {
  name: "personne",
  data() {
    return {
      currentPersonne: null,
      message: ''
    };
  },
  methods: {
    getPersonne(id) {
      PersonneDataService.get(id)
        .then(response => {
          this.currentPersonne = response.data;
          console.log(response.data);
        })
        .catch(e => {
          console.log(e);
        });
    },

    updatePersonne() {
      PersonneDataService.update(this.currentPersonne)
        .then(response => {
          console.log(response.data);
          this.message = 'Personne modifiée avec succès!';
        })
        .catch(e => {
          console.log(this.currentPersonne);
          console.log(e);
        });
    },

    deletePersonne() {
      PersonneDataService.delete(this.currentPersonne.id)
        .then(response => {
          console.log(response.data);
          this.$router.push({ name: "personnes" });
        })
        .catch(e => {
          console.log(e);
        });
    }
  },
  mounted() {
    this.message = '';
    this.getPersonne(this.$route.params.id);
  }
};
</script>

<style>
.edit-form {
  max-width: 300px;
  margin: auto;
}
</style>
