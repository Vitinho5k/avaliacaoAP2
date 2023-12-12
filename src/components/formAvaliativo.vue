<template>
    <div id="app" class="form-container">
      <div class="form1">
        <h2> FORMULÁRIO </h2>
        <div class="form-tela">
          <label for="name">Nome completo: </label> 
          <input type="text" id="name" placeholder="Insira seu Nome aqui" v-model="name" :class="{ 'is-invalid': !nameValid }"/> 
        </div>
        <div class="form-tela">
          <label for="email">Endereço de e-mail: </label> 
          <input type="email" id="email" placeholder="Insira seu Email aqui" v-model="email" :class="{ 'is-invalid': !emailValid }"/> 
        </div>
        <div class="form-tela">
          <label for="age">Idade: </label> 
          <input type="number" id="age" placeholder="insira sua Idade aqui" v-model="age" :class="{ 'is-invalid': !ageValid }"/> 
        </div>
        <div class="form-tela">
          <label for="description">Uma Breve Descrição de si mesmo:</label> 
          <textarea id="description" placeholder="Insira sua Descrição aqui" v-model="description" :class="{ 'is-invalid': !descriptionValid }"></textarea>
        </div>
        <div class="form-buttons">
          <button type="button" @click="validateAndSubmitForm" :disabled="formSubmitted" class="btn btn-primary"> {{ formSubmitted ? 'Enviado' : 'Enviar' }}
          </button>
          <button type="button" @click="clearForm" class="btn btn-secondary"> Limpar </button>
        </div>
      </div>
      <div class="submitted-data" v-if="formSubmitted">
        <h3> Dados do formulário </h3>
        <ul>
          <strong>Nome:</strong> {{ submittedData.name }} <br>
          <strong>E-mail:</strong> {{ submittedData.email }} <br>
          <strong>Idade:</strong> {{ submittedData.age }} <br>
          <strong>Descrição:</strong> {{ submittedData.description }} <br>
        </ul>
      </div>
    </div>
  </template>
  <script>
  export default {
    name:"formAvaliativo",
    data() {
      return {
        name: "",
        email: "",
        age: null,
        description: "",
        nameValid: true,
        emailValid: true,
        ageValid: true,
        descriptionValid: true,
        formSubmitted: false,
        submittedData: {
          name: "",
          email: "",
          age: null,
          description: "",
        },
      };
    },
    methods: {
      validateAndSubmitForm() {
        this.nameValid = !!this.name;
        this.emailValid = /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(this.email); 
        this.ageValid = !isNaN(this.age) && this.age > 0;
        this.descriptionValid = !!this.description;
  
        if (this.nameValid && this.emailValid && this.ageValid && this.descriptionValid) {
          this.submitForm();
        } else {
          alert("Por favor, preencha todos os campos corretamente.");
        }
      },
      submitForm() {
        const userData = {
          name: this.name,
          email: this.email,
          age: this.age,
          description: this.description,
        };
        this.submittedData = userData;
        this.formSubmitted = true;
      },
      clearForm() {
        this.name = "";
        this.email = "";
        this.age = null;
        this.description = "";
        this.nameValid = true;
        this.emailValid = true;
        this.ageValid = true;
        this.descriptionValid = true;
        this.formSubmitted = false;
        this.submittedData = {
          name: "",
          email: "",
          age: null,
          description: "",
        };
      },
    },
  };
  </script>
  
  <style scoped>
  .form1 {
    width: 700px;
    background-color: #888888; 
    color: #3498db; 
    border-radius: 16px;
    padding: 30px;
  }

  h2 {
    color: #000000; 
  }

  h3 {
    color: #3498db; 
  }

  .form-container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: #ffffff; 
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }

  .form {
    max-width: 400px;
    width: 100%;
    padding: 40px;
    background-color: #d8d8d8; 
    border-radius: 16px;
    box-shadow: 0 0 10px #07006e; 
  }

  .form-tela {
    margin-bottom: 20px;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  label {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    margin-bottom: 10px;
    color: #000000; 
  }

  input,
  textarea {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    width: 100%;
    padding: 10px;
    border: 1px solid #000551; 
    border-radius: 4px;
    color: #2c3e50; 
    background-color: #ffffff; 
  }

  .form-control {
    width: 100%;
    padding: 10px;
    font-size: 14px;
    border: 1px solid #3498db; 
    border-radius: 4px;
    box-sizing: border-box;
  }

  button {
    width: 48%;
    padding: 12px;
    font-size: 16px;
    margin-right: 4%;
    margin-bottom: 10px;
    cursor: pointer;
    border-radius: 4px;
    background-color: #020259; 
    border: 1px solid #000000; 
    color: #ffffff; 
  }

  .form-buttons {
    display: flex;
    justify-content: space-between;
  }

  strong {
    color: #000000; 
  }

  .submitted-data {
    margin-top: 10px;
    text-align: left;
    padding: 20px;
    border: 1px solid #02003e; 
    border-radius: 8px;
    width: auto;
    box-shadow: 0 0 10px #02003e; 
  }

  .is-invalid {
    border: 1px solid red;
  }
</style>
