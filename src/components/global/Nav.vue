<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="dark">
      <b-navbar-brand class="logo" href="/"
        ><img src="/images/logo/computhand.png"
      /></b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item href="/">
            <b-icon-house-door></b-icon-house-door> Home
          </b-nav-item>
          <b-nav-item
            href="https://www.linkedin.com/in/vincent-baylly-484a0070/"
            target="_blank"
          >
            <b-icon-person-lines-fill></b-icon-person-lines-fill> Auteur
          </b-nav-item>
          <b-nav-item href="/trainings">
            <b-icon-book></b-icon-book> Formation offerte
          </b-nav-item>
          <b-nav-item href="/skills">
            <b-icon-screwdriver></b-icon-screwdriver> Competence
          </b-nav-item>
          <b-nav-item href="/projects">
            <b-icon-laptop></b-icon-laptop> Projets
          </b-nav-item>
          <b-nav-item href="/contact">
            <b-icon-envelope></b-icon-envelope> Contact
          </b-nav-item>
        </b-navbar-nav>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-nav-item-dropdown text="Lang" right>
            <b-dropdown-item href="#">EN</b-dropdown-item>
            <b-dropdown-item href="#">FR</b-dropdown-item>
          </b-nav-item-dropdown>

          <!-- connexion menu -->
          <b-nav-item href="/login" v-if="isLogged === false">
            LogIn
          </b-nav-item>

          <b-nav-form>
            <b-button
              href="/signin"
              size="sm"
              class="my-2 my-sm-0"
              variant="outline-secondary"
              v-if="isLogged === false"
              >SignIn</b-button
            >
          </b-nav-form>

          <!-- logged In menu -->
          <b-nav-item-dropdown v-if="isLogged === true" right>
            <template v-slot:button-content>
              <em>User</em>
            </template>
            <b-dropdown-item href="training/dashboard"
              >Tableau de bord</b-dropdown-item
            >
            <b-dropdown-item @click.prevent="signOut">Sign Out</b-dropdown-item>
          </b-nav-item-dropdown>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>
<style>
.logo {
  display: block;
  background: #8a0808;
  border-radius: 50%;
  overflow: hidden;
  width: 50px;
  height: 50px;
  margin: auto;
  border: 2px solid white;
}

.logo img {
  max-width: 100%;
  margin-top: 5%;
}
</style>
<script>
import auth from "../helper/auth.js";

export default {
  template: "<Navigation/>",
  name: "navigation",
  mixins: [auth],
  data() {
    return {
      isLogged: this.checkTokenValidity(),
    };
  },
  created() {
    this.$on("loggedIn", () => {
      this.isLogged = this.checkTokenValidity();
    });
  },
  methods: {
    signOut() {
      this.isLogged = this.unvalidateToken();
      this.$router.push("/");
    },
  },
};
</script>
