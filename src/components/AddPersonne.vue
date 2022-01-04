<template>
  <div class="submit-form">
    <div v-if="!submitted">
      <div class="form-group">
        <label for="id">ID</label>
        <input
          type="text"
          class="form-control"
          id="id"
          required
          v-model="personne.id"
          name="id"
        />
      </div>

      <div class="form-group">
        <label for="name">Nom</label>
        <input
          type="text"
          class="form-control"
          id="name"
          required
          v-model="personne.name"
          name="name"
        />
      </div>

      <div class="form-group">
        <label for="surname">Prénom</label>
        <input
          type="text"
          class="form-control"
          id="surname"
          required
          v-model="personne.surname"
          name="surname"
        />
      </div>

      <div class="form-group">
        <label for="phone">Téléphone</label>
        <input
          type="text"
          class="form-control"
          id="phone"
          required
          v-model="personne.phone"
          name="phone"
        />
      </div>

      <div class="form-group">
        <label for="city">Ville</label>
        <input
          type="text"
          class="form-control"
          id="city"
          required
          v-model="personne.city"
          name="city"
        />
      </div>

      <button @click="creerPersonne" class="btn btn-success">Ajouter</button>
    </div>

    <div v-else>
      <h4>Personne ajoutée avec succès!</h4>
      <button class="btn btn-success" @click="resetForm">Ajouter une nouvelle personne</button>
    </div>
  </div>
</template>

<script>
import PersonneDataService from "../services/PersonneDataService";

export default {
  name: "add-personne",
  data() {
    return {
      personne: {
        id: null,
        name: "",
        surname: "",
        phone: "",
        city: ""
      },
      submitted: false
    };
  },
  methods: {
    creerPersonne() {
      var data = {
        id: this.personne.id,
        name: this.personne.name,
        surname: this.personne.surname,
        phone: this.personne.phone,
        city: this.personne.city
      };

      PersonneDataService.create(data)
        .then(response => {
          console.log(response.data);
          this.submitted = true;
        })
        .catch(e => {
          console.log(e);
        });
    },
    
    resetForm() {
      this.submitted = false;
      this.personne = {};
    }
  }
};
</script>

<style>
.submit-form {
  max-width: 300px;
  margin: auto;
}
</style>
