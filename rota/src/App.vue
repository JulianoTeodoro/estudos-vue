<template>
  <div id="app">
    
    <div class="jumbotron">
      <h1 class="display-4">Vue Router</h1>
      <p class="lead">Adicionando rotas a Single Page Applications no Vue.</p>
    </div>

    <div class="container">
      <router-link to="/home" class="btn btn-info mb-2 mr-2" exact>Home</router-link>
      <router-link to="/contatos" class="btn btn-secondary mb-2 mr-2" exact>Contatos</router-link>

      <transition name="slide" mode="out-in">
          <router-view></router-view>
      </transition>
    </div>

  </div>
</template>

<style scoped>
  .slide-enter, .slide-leave-to {
    transform: translate(-50px);
    opacity: 0
  }

  .slide-enter-active, .slide-leave-active{
    transition: all 0.3s;
  }
</style>