<template>
  <button @click="page = page - 1" class="back-button" v-if="page !== 1">
      <i class="fs-2 fa fa-angle-left" style="color: #483698"></i>
  </button>

  <main :class="{ firstPageBackground: page === 1, secondPageBackground: page === 2 }" class="main-container shadow w-75">

    <form v-if="page === 1" class="w-50 d-flex justify-content-center align-items-start flex-column">
      <h1 class="fs-1">Sobre o profissional</h1>
      <p class="fs-5 mt-4 fw-bold">Dados do profissional</p>

      <label class="mt-4 form-label">Nome completo*</label>
      <input :class="{ invalidInput: errors.name }" type="text" v-model="name" minlength="3" maxlength="48" placeholder="Digite o nome completo" />
      <p class="mt-2 mb-0 invalidText" v-show="errors.name">Nome precisa possuir mais que 3 caracteres.</p>

      <label class="mt-4 form-label">CPF*</label>
      <input :class="{ invalidInput: errors.cpf }" class="w-75" v-model="cpf" v-maska="'###.###.###-##'" type="text" placeholder="Digite um CPF" />
      <p class="mt-2 mb-0 invalidText" v-show="errors.cpf">CPF inválido.</p>

      <label class="mt-4 form-label">Número de celular*</label>
      <input :class="{ invalidInput: errors.phone }" class="w-75" v-model="phone" type="text" v-maska="'(##) # ####-####'" placeholder="(00) 0 0000-0000" />
      <p class="mt-2 mb-0 invalidText" v-show="errors.phone">Número de celular inválido.</p>

      <div class="mt-4 d-flex justify-content-between align-items-start w-100">
        <div>
          <label class="form-label">Estado*</label>
          <select :class="{ invalidInput: errors.uf }" class="p-1" v-model="uf" @change="changeCityOptions(uf)">
            <option value="" disabled selected>Selecione</option>
            <option value="0">Paraná</option>
            <option value="1">Rio Grande do Sul</option>
            <option value="2">Santa Catarina</option>
          </select>
          <p class="mt-2 mb-0 invalidText" v-show="errors.uf">Selecione um estado.</p>
        </div>

        <div>
          <label class="form-label">Cidade*</label>
          <select :class="{ invalidInput: errors.city }" class="p-1" v-model="city">
            <option value="" disabled selected>Selecione</option>
            <option v-for="option in cityOptions" :value="option" :key="option">{{option}}</option>
          </select>
          <p class="mt-2 mb-0 invalidText" v-show="errors.city">Selecione uma cidade.</p>
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

      <button type="button" @click="nextStep()" class="mt-2 w-100 p-1">PRÓXIMO</button>
    </form>
    
    <form v-if="page === 2" class="w-50 d-flex justify-content-center align-items-start flex-column">
      <h1 class="fs-1">Sobre o atendimento </h1>
      <p class="fs-5 mt-4 fw-bold">Detalhes do atendimento</p>

      <label class="mt-4 form-label">Especialidade principal*</label>
      <input :class="{ invalidInput: errors.name }" type="text" v-model="name" minlength="3" maxlength="48" placeholder="Digite o nome completo" />
      <p class="mt-2 mb-0 invalidText" v-show="errors.name">Nome precisa possuir mais que 3 caracteres.</p>

      <label class="mt-4 form-label">Informe o preço da consulta*</label>
      <div class="input-group mb-3">
        <span class="input-group-text" id="basic-addon1">R$</span>
        <input type="text" style="width: 50% !important" placeholder="Valor" aria-label="Valor" aria-describedby="basic-addon1">
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
        </div>
        <p class="m-0 fs-5">2 de 2</p>
      </div>
      <button type="button" @click="nextStep()" class="mt-2 w-100 p-1">PRÓXIMO</button>
    </form>
  </main>
</template>

<script>
export default {
  name: "Main",
  data() {
    return {
      errors: {
        name: false,
        cpf: false,
        phone: false,
        uf: false,
        city: false,
      },
      name: null,
      cpf: null,
      phone: null,
      uf: '',
      city: '',
      cityOptions: [],
      page: 1,
    }
  },
  methods: {
    changeCityOptions(uf) {
      switch (uf) {
        case "0":
          this.cityOptions = ['Londrina', 'Maringá'];
          break;
      
        case "1":
          this.cityOptions = ['Pelotas', 'Porto Alegre'];
          break;
        
        case "2":
          this.cityOptions = ['Florianópolis', 'Joinville'];
          break;
      }
    },

    nextStep() {
      switch (this.page) {
        case 1:
          !this.name ? this.errors.name = true : this.name.length < 3 ? this.errors.name = true : this.errors.name = false;
          !this.cpf ? this.errors.cpf = true : this.cpf.length < 14 ? this.errors.cpf = true : this.errors.cpf = false;
          !this.phone ? this.errors.phone = true : this.phone.length < 16 ? this.errors.phone = true : this.errors.phone = false;
          this.uf === '' ? this.errors.uf = true : this.errors.uf = false;
          this.city === '' ? this.errors.city = true : this.errors.city = false;
          this.errors.name || this.errors.cpf || this.errors.phone || this.errors.uf || this.errors.city ? this.page = 1 : this.page = 2;
          break;
      }
    }
  },
};
</script>

<style scoped>
.back-button {
  position: fixed;
  top: 5rem;
  left: 15%;
  background: none;
  border: none;
  outline: none;
}

.main-container {
  border-radius: 1.5rem;
  padding: 2rem 5rem;
  background-repeat: no-repeat;
  background-position-x: right;
  background-position-y: center;
  background-size: 27rem;
  background-color: #fff;
}

.firstPageBackground {
  background-image: url("../assets/desktop-pagina-1.png");
}

.secondPageBackground {
  background-image: url("../assets/desktop-pagina-2.png");
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

#basic-addon1 {
  background-color: #483698;
  color: #fff;
}
</style>
