<template>
  <div id="app">
    <nav class="navbar sticky-top navbar-expand-lg navbar-dark bg-dark">
      <div class="container-fluid">
        <a class="navbar-brand" href="/movies">
          <img src="./assets/logo.png" alt="" width="40" height="40" />
          MOVIES!
        </a>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNavDropdown"
          aria-controls="navbarNavDropdown"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNavDropdown">
          <ul class="navbar-nav">
            <li class="nav-item">
              <a class="nav-link active" aria-current="page" href="/">Home</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="/movies">Movies</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="/movies/new">Add a Movie</a>
            </li>
          </ul>
          <ul class="navbar-nav ms-auto">
            <li class="nav-item dropdown">
              <a
                class="nav-link dropdown-toggle"
                href="#"
                id="navbarDropdownMenuLink"
                role="button"
                data-bs-toggle="dropdown"
                aria-expanded="false"
              >
                {{ currentUser.email || "Sign In" }}
              </a>
              <ul class="dropdown-menu" aria-labelledby="navbarDropdownMenuLink">
                <li><a class="dropdown-item" href="/login" v-if="!isLoggedIn()">Login</a></li>
                <li><a class="dropdown-item" href="/signup" v-if="!isLoggedIn()">Signup!</a></li>
                <li><a class="dropdown-item" href="/logout" v-if="isLoggedIn()">Logout</a></li>
              </ul>
            </li>
          </ul>
        </div>
      </div>
    </nav>
    <!-- <div id="nav">
      <router-link to="/">Home</router-link>
      |
      <router-link to="/about">About</router-link>
      |
      <router-link to="/movies">Movies</router-link>
      |
      <router-link to="/movies/new">New Movie</router-link>
      |
      <router-link to="/signup">Signup</router-link>
      |
      <router-link to="/login">Login</router-link>
      |
      <router-link to="/logout">Logout</router-link>
    </div> -->

    <router-view @updateParent="handleUpdate" />
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      currentUser: { email: localStorage.getItem("email") },
    };
  },
  methods: {
    handleUpdate: function (value) {
      this.currentUser.email = value;
    },
    isLoggedIn: function () {
      if (localStorage.getItem("email")) return true;
      else return false;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
