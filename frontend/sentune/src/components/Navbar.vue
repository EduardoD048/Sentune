<template>
  <nav class="navbar">
    <!-- Logo -->
    <div class="logo">
      <img src="@/assets/logo.svg" alt="Sentune Logo" title=""/>
    </div>

    <!-- barra de pesquisa -->
    <div class="search-container">
      <div class="search-input-wrapper">
        <img src="@/assets/search.svg" alt="pesquisar" title="pesquisar" />
        <input
          type="text"
          name="search-music"
          class="search-input"
          placeholder="oque você quer ouvir?"
        />
      </div>
    </div>

    <!-- controle do usuário -->
    <button class="premium-button">Ver planos Premium</button>
   <div class="notification">
    <img src="@/assets/notification.svg" alt="notificação" title="notificação" />
   </div>
  </nav>
</template>

<script setup>
// Lógica do componente pode ser adicionada aqui
</script>

<style scoped>
.navbar {
  background-color: #121212;
  color: #b3b3b3;
  height: 76px;
  padding: 12px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  position: sticky;
  top: 0;
  z-index: 100;
  width: 100vw;
}

.logo img {
    width: 36px;
    height: 36px;
    margin-right: 10px;
}

.logo {
  display: flex;
  align-items: center;
  font-size: 24px;
  color: #b3b3b3;
}

.search-container {
  flex-grow: 1;
  display: flex;
  justify-content: center;
}

.search-input-wrapper {
  position: relative;
  width: 50%;
  display: flex;
  align-items: center;
  background-color: #5a5a5a;
  border-radius: 500px;
  padding: 10px;
}

.search-input {
  background: transparent;
  border: none;
  color: white;
  font-size: 20px;
  outline: none;
  width: 100%;
  padding: 0 8px;
}

.search-input::placeholder {
  color: #b3b3b3;
}

/* Estilização para o ícone de busca */
.search-input-wrapper img {
  width: 28px;
  height: 28px;
  margin-right: 8px;
}

.search-input-wrapper:hover {
  background-color: #727272;
  transition: 0.5s;
}

.premium-button {
  background-color: #727272;
  color: white;
  border: none;
  border-radius: 50px;
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
}
</style>
