<template>
  <div class="container mt-5">
    <form @submit.prevent="handleSubmit">
      <div class="form-row">
        <div class="col-md-5 mb-3">
          <label for="username" class="h5 font-weight-bold">Nom d'utilisateur</label>
          <input type="text" class="form-control border-secondary" id="username" v-model="username" placeholder="Choisissez un nom d'utilisateur"/>
        </div>
        <div class="col-md-5 mb-3">
          <label for="department" class="h5 font-weight-bold">Fonction</label>
          <input type="text" class="form-control border-secondary" id="department" v-model="department" placeholder="Dans quel secteur de l'entreprise travaillez vous ?"/>
        </div>
      </div>
      <button type="submit" class="btn btn-primary btn-block col-9 col-sm-4 col-lg-3 mt-3 mx-auto mx-sm-0">Enregistrer</button>
    </form>
  </div>
</template>

<script>

import axios from 'axios'
import { mapState } from 'vuex'
import '../axios'

export default ({
    name: 'ModifyPost',

    data() {
        return{
            username: '',
            department: '',
        }
    },

    computed: {
        ...mapState(['user']),
    },

    methods: {
        async handleSubmit() {
        const response =  await axios.put('users/me', {
            username: this.username,
            department: this.department,
        })
        console.log(response)
        const res = await axios.get('users/me')
        this.$store.dispatch('user', res.data)
        this.$router.push('/profil')
    }
  }
})
</script>

<style>

</style>