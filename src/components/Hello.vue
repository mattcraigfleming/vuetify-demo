<template>
  <div class="hello">
    <v-dialog v-model="modelOpen">
      <v-btn primary dark slot="activator">Create Profile</v-btn>
      <v-card>
        <v-card-row>
          <v-card-title>User Profile</v-card-title>
        </v-card-row>
        <v-card-row>
          <v-card-text>
            <v-container fluid>
              <v-text-field label="Email" :rules="emailRules" v-model="profile.email" required />
              <v-text-field label="Password" type="password" required />
              <v-text-field label="Legal first name" required />
              <v-text-field label="Legal middle name" hint="example of helper text only on focus" />
              <v-text-field label="Legal last name" hint="example of persistent helper text"
                persistent-hint
                required />
              <small>*indicates required field</small>
            </v-container>
          </v-card-text>
        </v-card-row>
        <v-card-row actions>
          <v-btn class="blue--text darken-1" flat @click.native="modelOpen = false">Close</v-btn>
          <v-btn class="blue--text darken-1" flat @click.native="modelOpen = false">Save</v-btn>
        </v-card-row>
      </v-card>
    </v-dialog>
    <v-expansion-panel expand>
      <v-expansion-panel-content v-for="(gif,i) in giphys" :key="i">
        <div slot="header"><p class="text-xs-center">{{gif.embed_url}}</p></div>
        <v-card>
          <v-card-text class="grey lighten-3 text-xs-center"><img :src="gif.images.original.url" class="img__responsive" /></v-card-text>
        </v-card>
      </v-expansion-panel-content>
    </v-expansion-panel>
    <div>
      <div class="portrait" v-for="gif in giphys">
      <v-card :img="gif.images.original.url" height="700px">
        <v-card-row actions class="white--text pl-3 pt-3 pb-3">{{gif.embed_url}}</v-card-row>
      </v-card>
    </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data() {
    return {
      msg: 'Welcome to Your Vue.js App',
      giphys: [],
      profile: {
        email: '',
      },
      modelOpen: true,
      emailRules: [(email) => {
        console.log('email', email);
        return email === 'mfleming@zonedigital.com';
      }],
    };
  },
  mounted() {
    this.load();
  },
  methods: {
    load() {
      fetch('http://api.giphy.com/v1/gifs/search?q=funny+cat&api_key=dc6zaTOxFJmzC', {
        headers: {
          Authorization: 'dc6zaTOxFJmzC',
        },
      })
     .then(res => res.json())
     .then((result) => {
       console.log(result.data);
       this.giphys = result.data;
     });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .img__responsive {
    width:20%;
    height:auto;
  }
</style>
