<template>
  <button @click="page = page - 1" class="back-button" v-if="page !== 1 && page !== 4">
      <i class="fs-2 fa fa-angle-left" style="color: #483698"></i>
  </button>

  <main :class="{ firstPageBackground: page === 1, secondPageBackground: page === 2, thirdPageBackground: page === 3 }" class="main-container shadow w-75">

    <form v-if="page === 1" class="w-50 d-flex justify-content-center align-items-start flex-column">
      <h1 class="fs-1 fw-bold">Sobre o profissional</h1>
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
            <option value="Paraná">Paraná</option>
            <option value="Rio Grande do Sul">Rio Grande do Sul</option>
            <option value="Santa Catarina">Santa Catarina</option>
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

      <Button :btnSecondary="false" :btnPrimary="true" :text="'PRÓXIMO'" @click="nextStep()" class="mt-2 w-100 p-1" />
    </form>
    
    <form v-if="page === 2" class="w-50 d-flex justify-content-center align-items-start flex-column">
      <h1 class="fs-1 fw-bold">Sobre o atendimento </h1>
      <p class="fs-5 mt-4 fw-bold">Detalhes do atendimento</p>

      <label class="form-label">Especialidade principal*</label>
      <select :class="{ invalidInput: errors.specialism }" class="p-1" v-model="specialism">
        <option value="" disabled selected>Selecione a especialidade</option>
        <option v-for="option in specialismOptions" :value="option" :key="option">{{option}}</option>
      </select>
      <p class="mt-2 mb-0 invalidText" v-show="errors.specialism">Selecione uma especialidade.</p>

      <label class="mt-4 form-label">Informe o preço da consulta*</label>
      <div class="input-group">
        <span class="input-group-text" id="basic-addon1">R$</span>
        <input v-model="price" :class="{ invalidInput: errors.price }" v-maska="['##,##', '###,##']" type="text" class="w-50 border-start-0" placeholder="Valor" aria-label="Valor" aria-describedby="basic-addon1">
      </div>
      <p class="mt-2 mb-0 invalidText" v-show="errors.price">Preço mínimo de R$30,00 e máximo de R$ 350,00.</p>

      <label class="mt-4 form-label">Formas de pagamento da consulta*</label>
      <div class="w-100 d-flex align-items-start justify-content-start flex-column">
        <div class="shadow ps-5 p-3 w-100 mt-4 payments-item">
          <label class="checkbox-container d-flex"><strong>Pix</strong>
            <input type="checkbox" v-model="pix">
            <span :class="{ invalidInput: errors.payments }" class="custom-checkbox"></span>
          </label>
        </div>

        <div class="shadow ps-5 p-3 w-100 mt-4 payments-item">
          <label class="checkbox-container d-flex"><strong>Em dinheiro</strong>
            <input type="checkbox" v-model="money">
            <span :class="{ invalidInput: errors.payments }" class="custom-checkbox"></span>
          </label>
        </div>

        <div class="shadow ps-5 p-3 w-100 mt-4 payments-item">
          <label class="checkbox-container d-flex"><strong>Cartão de crédito</strong>
            <input type="checkbox" v-model="creditCard">
            <span :class="{ invalidInput: errors.payments }" class="custom-checkbox"></span>
          </label>

          <div class="mt-4" v-if="creditCard">
            <div class="form-check d-flex w-100">
              <input class="form-check-input" type="radio" v-model="installment" value="1x" name="installment" id="oneTime">
              <label class="form-check-label w-100 ms-4" for="oneTime">
                1x, sem juros
              </label>
            </div>
            <div class="form-check d-flex w-100">
              <input class="form-check-input" type="radio" v-model="installment" value="2x" name="installment" id="twoTimes">
              <label class="form-check-label w-100 ms-4" for="twoTimes">
                2x, sem juros
              </label>
            </div>
            <div class="form-check d-flex w-100">
              <input class="form-check-input" v-model="installment" type="radio" value="3x" name="installment" id="threeTimes">
              <label class="form-check-label w-100 ms-4" for="threeTimes">
                3x, sem juros
              </label>
            </div> 
          </div>
        </div>
      </div>
      <p class="mt-2 mb-0 invalidText" v-show="errors.payments">Selecione uma forma de pagamento.</p>
      <p class="mt-2 mb-0 invalidText" v-show="errors.installment">Selecione quantidade de parcelamento.</p>

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
      <Button :btnSecondary="false" :btnPrimary="true" :text="'PRÓXIMO'" @click="nextStep()" class="mt-2 w-100 p-1" />
    </form>

    <div v-if="page === 3" class="w-50 d-flex justify-content-center align-items-start flex-column">
      <h1 class="fs-1 fw-bold">Revisão do cadastro</h1>

      <p class="fs-5 mt-4 mb-0 fw-bold">Nome completo</p>
      <p class="fs-5 m-0">{{ name }}</p>

      <p class="fs-5 mt-4 mb-0 fw-bold">CPF</p>
      <p class="fs-5 m-0">{{ cpf }}</p>

      <p class="fs-5 mt-4 mb-0 fw-bold">Número de celular ou telefone</p>
      <p class="fs-5 m-0">{{ phone }}</p>

      <p class="fs-5 mt-4 mb-0 fw-bold">Estado/Cidade</p>
      <p class="fs-5 m-0">{{ uf }} - {{ city }}</p>

      <p class="fs-5 mt-4 mb-0 fw-bold">Especialidade principal</p>
      <p class="fs-5 m-0">{{ specialism }}</p>

      <p class="fs-5 mt-4 mb-0 fw-bold">Preço da Consulta</p>
      <p class="fs-5 m-0">R$ {{ price }}</p>

      <p class="fs-5 mt-4 mb-0 fw-bold">Formas de pagamento da consulta</p>
      <p class="fs-5 m-0" v-show="pix">Pix</p>
      <p class="fs-5 m-0" v-show="money">Em dinheiro</p>
      <p class="fs-5 m-0" v-show="creditCard">Cartão de crédito - Parcelamento em {{ installment }} sem juros</p>

      <Button :btnPrimary="false" :btnSecondary="true" :text="'CADASTRAR PROFISSIONAL'" @click="page = 4" class="mt-5 p-2 w-100 p-1" />
      <h2 class="mt-5 fs-4 w-100 fw-bold text-center" style="cursor: pointer" @click="page = 1">Editar cadastro</h2>

    </div>

    <div v-if="page === 4">
      <h1 class="fs-1 fw-bold">Cadastro concluído!</h1>
      <p class="fs-5 mt-4 fw-bold">Agradecemos sua disponibilidade de facilitar a vida das pessoas.</p>
    </div>
  </main>
</template>

<script>
import Button from '../components/Button.vue';

export default {
  name: "Main",
  components: {
    Button,
  },
  data() {
    return {
      errors: {
        name: false,
        cpf: false,
        phone: false,
        uf: false,
        city: false,
        specialism: false,
        price: false,
        payments: false,
        installment: false,
      },
      name: null,
      cpf: null,
      phone: null,
      uf: '',
      city: '',
      cityOptions: [],
      specialism: '',
      price: '',
      pix: false,
      money: false,
      creditCard: false,
      specialismOptions: ['Cardiologia', 'Dermatologia', 'Neurologia', 'Oftalmologia', 'Psiquiatria', 'Urologia'],
      installment: null,
      page: 1,
    }
  },
  methods: {
    changeCityOptions(uf) {
      switch (uf) {
        case "Paraná":
          this.cityOptions = ['Londrina', 'Maringá'];
          break;
      
        case "Rio Grande do Sul":
          this.cityOptions = ['Pelotas', 'Porto Alegre'];
          break;
        
        case "Santa Catarina":
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

        case 2:
          this.specialism === '' ? this.errors.specialism = true : this.errors.specialism = false;
          Number(this.price.replace(',','.')) < 30.00 || Number(this.price.replace(',','.')) > 350.00 ? this.errors.price = true : this.errors.price = false;
          !this.pix && !this.money && !this.creditCard ? this.errors.payments = true : this.errors.payments = false;
          this.creditCard ? !this.installment ? this.errors.installment = true : this.errors.installment = false : '';
          this.errors.specialism || this.errors.price || this.errors.payments || this.errors.installment ? this.page = 2 : this.page = 3;
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

.thirdPageBackground {
  background-image: url("../assets/desktop-pagina-3.png");
}

.main-container div div {
  width: 48%;
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

.payments-item {
  background-color: #f9f9f9;
  border-radius: 0.25rem;
}

input[type=checkbox] {
  visibility: hidden;
  width: 10%;
}

.checkbox-container {
  display: block;
  position: relative;
  padding-left: 45px;
  cursor: pointer;
}

.custom-checkbox {
  position: absolute;
  top: 0;
  left: 0;
  height: 25px;
  width: 25px;
  border-radius: 0.25rem;
  border: 1px solid #483698;
  background-color: #fff;
}

.checkbox-container input:checked ~ .custom-checkbox {
  background-color: #483698;
}

.custom-checkbox:after {
  content: "";
  position: absolute;
  display: none;
}
          
.checkbox-container input:checked ~ .custom-checkbox:after {
  display: block;
}

.checkbox-container .custom-checkbox:after {
  left: 8px;
  bottom: 7px;
  width: 6px;
  height: 12px;
  border: solid white;
  border-width: 0 4px 4px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}
</style>
