<template>
  <div class="main-container shadow">
    <h1 class="fs-1">Sobre o profissional</h1>
    <form class="d-flex justify-content-center align-items-start flex-column">
      <p class="fs-5 mt-4 fw-bold">Dados do profissional</p>

      <label class="mt-2 form-label">Nome completo*</label>
      <input
        class="form-control"
        type="text"
        placeholder="Digite o nome completo"
      />

      <label class="mt-2 form-label">CPF*</label>
      <input class="form-control" type="text" placeholder="Digite um CPF" />

      <label class="mt-2 form-label">Número de celular*</label>
      <input class="form-control" type="text" placeholder="(00) 0 0000-0000" />

      <div class="mt-2 d-flex justify-content-between align-items-center">
        <label class="form-label">Estado*</label>
        <select class="form-select">
          <option value="">Selecione</option>
        </select>

        <label class="form-label">Estado*</label>
        <select class="form-select">
          <option value="">Selecione</option>
        </select>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "Main",
};
</script>

<style>
.main-container {
  background-color: #f9f9f9;
  border-radius: 1.5rem;
  padding: 2rem 5rem;
  width: 70vw;
}
</style>
