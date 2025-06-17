<template>
  <nav class="navbar">
    <!-- Logo -->
    <div class="logo">
      <img src="@/assets/logo.svg" alt="Sentune Logo" title=""/>
    </div>

    <!-- Conteúdo central: home + pesquisa -->
    <div class="center-content">

      <div class="home-button">
        <img src="@/assets/home.svg" alt="home" title="home" />
      </div>

      <!-- Barra de pesquisa -->
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

    <!-- Controles do usuário -->
    <div class="user-controls">
      <button class="premium-button">Ver planos Premium</button>
      <div class="notification">
        <img src="@/assets/notification.svg" alt="notificação" title="notificação" />
      </div>
    </div>
  </nav>
</template>

<style scoped>

/* Navbar principal */
.navbar {
  background-color: #121212;
  color: #b3b3b3;
  height: 76px;
  padding: 0 16px;
  display: flex;
  align-items: center;
  width: 100%;
}

/* Logo */
.logo {
  margin-right: 16px;
}

.logo img {
  width: 36px;
  height: 36px;
}

/* Conteúdo central */
.center-content {
  display: flex;
  align-items: center;
  flex: 1; 
  max-width: 600px; 
  margin: 0 auto;
}

/* Botão home */
.home-button {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-right: 16px;
}

.home-button img {
  width: 24px;
  height: 24px;
}

/* Barra de pesquisa */
.search-input-wrapper {
  display: flex;
  align-items: center;
  background-color: #fff;
  border-radius: 500px;
  padding: 8px 12px;
  width: 100%;
}

.search-input-wrapper img {
  width: 16px;
  height: 16px;
  margin-right: 8px;
}

.search-input {
  border: none;
  background: transparent;
  width: 100%;
  outline: none;
  font-size: 14px;
}

/* Controles de usuário */
.user-controls {
  display: flex;
  align-items: center;
  gap: 16px;
}

.premium-button {
  background: transparent;
  border: 1px solid #b3b3b3;
  border-radius: 500px;
  color: white;
  padding: 8px 16px;
  font-size: 14px;
  font-weight: 700;
  cursor: pointer;
}

.notification {
  display: flex;
}

.notification img {
  width: 24px;
  height: 24px;
}

</style>