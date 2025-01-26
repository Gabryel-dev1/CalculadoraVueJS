<template>
  <div id="app" class="calculadora">
    <h1>Calculadora Aritmética</h1>

    <input type="number" v-model.number="numero1" placeholder="Digite o primeiro número" />

    <input type="number" v-model.number="numero2" placeholder="Digite o segundo número" />

    <div class="operacoes">
      <button v-for="operacao in operacoes" :key="operacao.id" :class="{ ativo: operacao.id === operacaoSelecionada }"
        @click="selecionarOperacao(operacao.id)">
        {{ operacao.simbolo }}
      </button>
    </div>

    <div class="resultado">
      <span>Resultado:</span>
      <strong>{{ resultado }}</strong>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      numero1: 0,
      numero2: 0,
      operacoes: [
        { id: "somar", simbolo: "+" },
        { id: "subtrair", simbolo: "-" },
        { id: "multiplicar", simbolo: "×" },
        { id: "dividir", simbolo: "÷" },
      ],
      operacaoSelecionada: "somar", // Operação padrão
    };
  },
  methods: {
    selecionarOperacao(id) {
      this.operacaoSelecionada = id;
    },
  },
  computed: {
    resultado() {
      // Calcula o resultado automaticamente
      switch (this.operacaoSelecionada) {
        case "somar":
          return this.numero1 + this.numero2;
        case "subtrair":
          return this.numero1 - this.numero2;
        case "multiplicar":
          return this.numero1 * this.numero2;
        case "dividir":
          return this.numero2 !== 0
            ? (this.numero1 / this.numero2).toFixed(2)
            : "Erro (Divisão por 0)";
        default:
          return "Operação inválida";
      }
    },
  },
};
</script>

<style scoped>
.calculadora {
  max-width: 400px;
  margin: 50px auto;
  padding: 20px;
  background: linear-gradient(145deg, #ffffff, #e6e6e6);
  border-radius: 15px;
  box-shadow: 4px 4px 8px #d1d1d1, -4px -4px 8px #ffffff;
  text-align: center;
  font-family: "Poppins", sans-serif;
}


h1 {
  font-size: 1.8rem;
  color: #333;
  margin-bottom: 20px;
}


input {
  width: calc(100% - 20px);
  margin: 10px 0;
  padding: 10px;
  font-size: 1rem;
  border: none;
  border-radius: 10px;
  background: #f0f0f0;
  box-shadow: inset 2px 2px 5px #d1d1d1, inset -2px -2px 5px #ffffff;
  outline: none;
  transition: all 0.2s ease-in-out;
}

input:focus {
  box-shadow: inset 2px 2px 5px #bdbdbd, inset -2px -2px 5px #ffffff;
}


.operacoes {
  display: flex;
  justify-content: space-around;
  margin: 15px 0;
}

.operacoes button {
  width: 60px;
  height: 60px;
  border: none;
  border-radius: 50%;
  font-size: 1.5rem;
  background: #f0f0f0;
  box-shadow: 4px 4px 8px #d1d1d1, -4px -4px 8px #ffffff;
  transition: all 0.2s ease-in-out;
  cursor: pointer;
}

.operacoes button.ativo {
  background: #4c66af;
  color: white;
  box-shadow: 4px 4px 8px #242372, -4px -4px 8px #5cd3c3;
}

.operacoes button:hover {
  background: #e0e0e0;
}

.operacoes button:active {
  box-shadow: inset 2px 2px 5px #bdbdbd, inset -2px -2px 5px #ffffff;
}


.resultado {
  margin-top: 20px;
  font-size: 1.2rem;
  color: #555;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.resultado span {
  font-size: 1rem;
  color: #888;
}

.resultado strong {
  font-size: 1.5rem;
  color: #333;
  margin-top: 5px;
}
</style>
