<template>
  <div>
    <p>Autor: {{ autor }}</p>
    <p :title="mensagem">{{ new Date().toLocaleString() }}</p>
    <button @click="maiuscula()">Mudar autor</button>

    <div>
      <h2>Projetos</h2>

      <button @click="mostraFormulario = true" v-show="!mostraFormulario">
        Formulario
      </button>

      <form @submit.prevent="salvar()" v-show="mostraFormulario">
        <label for="nome">Nome</label>
        <input type="text" id="nome" v-model="nome" size="30 required" /><br />
        <label for="duracao">Duração</label>
        <input type="number" id="duracao" v-model="duracao" required /><br />
        <input type="submit" value="Adicionar" /><br />

        {{ nome }}
        {{ duracao }}
      </form>
      <br />

      <input type="text" v-model="filtro" placeholder="Filtro" />
      <br />
      <button @click="ordenar()">Ordenar</button>

      <table>
        <tr>
          <th>Id</th>
          <th @click="ordenar">
            Nome
            <span v-if="ordened" class="material-symbols-outlined"
              >arrow_upward</span>
            <span v-else class="material-symbols-outlined">arrow_downward</span>
          </th>
          <th>Duração</th>
        </tr>
        <tr
          v-for="p in projetosfiltrados"
          :key="p.id"
          @click="selected = p"
          :class="{ selected: isSelected(p) }"
        >
          <td>{{ p.id }}</td>

          <td>{{ p.id }}</td>

          <td>{{ p.nome }}</td>

          <td>{{ p.duracao }} -- {{ isSelected(p) }}</td>

          <td><a href="#" @click="excluir(p)">Excluir</a></td>
          <td><a href="#" @click="editar(p)">Editar</a></td>

        </tr>
      </table>

      {{ selected }}
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // json javascript object notation
      autor: "Giulia",
      mensagem: "Meu primeiro app vue",
      maiusculaMinuscula: false,
      filtro: "",
      mostraFormulario: false,
      selected: null,
      projetos: [
        {
          id: 15,
          nome: "Projeto Java",
          duracao: 10,
        },
        {
          id: 3,
          nome: "Projeto Delphi",
          duracao: 11,
        },
        {
          id: 7,
          nome: "Projeto Phyton",
          duracao: 12,
        },
      ],
      nome: "",
      duracao: null,
    };
  },

  methods: {
    editar(p) {
      


    },    
    ordenar() {
      if (
        this.projetos.sort((a, b) => b.nome.localeCompare(a.nome)) &&
        this.ordened == false
      )
        this.ordened = true;
      else {
        this.projetos.sort((a, b) => a.nome.localeCompare(b.nome));

        this.ordened = false;
      }
    },
    isSelected(projeto) {
      return this.selected !== null && this.selected.id == projeto.id;
    },
    transformar() {
      this.autor = this.maiusculaMinuscula
        ? this.autor.toUpperCase()
        : this.autor.toLowerCase();
      this.maiusculaMinuscula = !this.maiusculaMinuscula;
    },

    maiuscula() {
      if (this.maiusculaMinuscula) {
        this.autor = this.autor.toUpperCase();
      } else {
        this.autor = this.autor.toLowerCase();
      }
      this.maiusculaMinuscula = !this.maiusculaMinuscula;
    },

    getMaiorId() {
      return this.projetos.reduce((a, b) => (a.id > b.id ? a : b), 0).id + 1;

      // let maiorId = 0
      // this.projetos.forEach(p => maiorId = p.id > maiorId ? p.id : maiorId)
      // return ++maiorId
    },

    salvar() {
      const achou = this.projetos.some((p) => p.nome == this.nome);
      if (achou) {
        alert("achou");
      } else {
        // let maiorId = 0
        // this.projetos.forEach(p => maiorId = p.id > maiorId ? p.id : maiorId)

        this.projetos.push({
          id: this.getMaiorId(),
          nome: this.nome,
          duracao: this.duracao,
        });
        this.nome = "";
        this.duracao = null;
        this.mostraFormulario = false;
      }

    
    },
    excluir(projeto) {
      this.projetos.splice(this.projetos.indexOf(projeto), 1);
    },
  },
  computed: {
    projetosfiltrados() {
      if (this.filtro.trim().length == 0) return this.projetos;
      return this.projetos.filter((p) =>
        p.nome.toLowerCase().includes(this.filtro.toLowerCase())
      );
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.material-symbols-outlined {
  font-variation-settings: "FILL" 0, "wght" 400, "GRAD" 0, "opsz" 48;
}

.selected {
  background-color: pink;
}
</style>
