<template>
  <main class="main-container shadow w-75">
    <h1 class="fs-1">Sobre o profissional</h1>
    <form
      class="w-50 d-flex justify-content-center align-items-start flex-column"
    >
      <p class="fs-5 mt-4 fw-bold">Dados do profissional</p>

      <label class="mt-4 form-label">Nome completo*</label>
      <input type="text" placeholder="Digite o nome completo" />

      <label class="mt-4 form-label">CPF*</label>
      <input class="w-75" type="text" placeholder="Digite um CPF" />

      <label class="mt-4 form-label">Número de celular*</label>
      <input class="w-75" type="text" placeholder="(00) 0 0000-0000" />

      <div class="mt-4 d-flex justify-content-between align-items-center w-100">
        <div>
          <label class="form-label">Estado*</label>
          <select class="p-1">
            <option value="">Selecione</option>
          </select>
        </div>

        <div>
          <label class="form-label">Estado*</label>
          <select class="p-1">
            <option value="">Selecione</option>
          </select>
        </div>
      </div>

      <div
        class="
          loading-bar-container
          mt-4
          d-flex
          justify-content-between
          align-items-center
          w-100
        "
      >
        <div class="w-75 d-flex justify-content-center align-items-center">
          <div class="w-100 h-100 rounded purple-bar"></div>
          <div class="w-100 h-100 rounded gray-bar"></div>
        </div>
        <p class="m-0 fs-5">1 de 2</p>
      </div>

      <button type="button" class="mt-2 w-100 p-1">PRÓXIMO</button>
    </form>
  </main>
</template>

<script>
export default {
  name: "Main",
};
</script>

<style scoped>
.main-container {
  background-color: #fff;
  background-image: url("../assets/desktop-pagina-1.png");
  background-repeat: no-repeat;
  background-position-x: right;
  background-position-y: center;
  background-size: 27rem;
  border-radius: 1.5rem;
  padding: 2rem 5rem;
}

.main-container div div {
  width: 48%;
}

.main-container button {
  border-radius: 0.75rem;
  background-color: #483698;
  color: #fff;
  font-weight: bold;
  border: none;
}

.loading-bar-container div {
  height: 3vh;
}

.loading-bar-container .purple-bar {
  background-color: #483698;
}

.loading-bar-container .gray-bar {
  background-color: #f9f9f9;
}

.loading-bar-container p {
  font-weight: bold;
  color: #483698;
  font-family: "Comfortaa", cursive;
}
</style>
