<template>
  <nav class="navbar navbar-expand-lg bg-primary">
    <!--a class="navbar-brand" href="/">Home</!--a--> 
    <a class="navbar-brand" href="/"> Agenda</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
    <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
      <div class="navbar-nav">
        <router-link to="/">Home</router-link> 
        <router-link to="/agenda"> Agenda</router-link>
      </div>
    </div>
  </nav>
  <router-view/>
</template>

<style lang="scss">

</style>
