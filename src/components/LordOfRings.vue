<template>
  <div class="container mt-5 bg-light rounded shadow" style="background-image: url('https://i.pinimg.com/originals/57/f7/06/57f70693c0778a29af6d2388f7edc4b0.jpg
'); background-size: cover; background-position: center; padding: 30px;">
    <h2 class="text-center text-white mb-4">Cadastro de Personagens - Senhor dos Anéis</h2>

    <form @submit.prevent="addPersonagem" class="mb-4 bg-white p-4 rounded shadow">
      <div class="form-group">
        <label for="nome">Nome do Personagem:</label>
        <input
          type="text"
          v-model="novoPersonagem.nome"
          class="form-control"
          placeholder="Insira o nome"
          required
        />
      </div>

      <div class="form-group">
        <label for="raca">Raça:</label>
        <input
          type="text"
          v-model="novoPersonagem.raca"
          class="form-control"
          placeholder="Ex: Elfo, Orc, Humano"
          required
        />
      </div>

      <div class="form-group">
        <label for="alianca">Aliança:</label>
        <select v-model="novoPersonagem.alianca" class="form-control" required>
          <option disabled value="">Escolha uma aliança</option>
          <option>Sociedade do Anel</option>
          <option>Orcs</option>
          <option>Elfos</option>
          <option>Homens</option>
        </select>
      </div>

      <button type="submit" class="btn btn-primary btn-block ">Cadastrar Personagem</button>
    </form>

    <h3 class="text-center text-white">Lista de Personagens</h3>
    <ul v-if="personagens.length" class="list-group">
      <li
        v-for="(personagem, index) in personagens"
        :key="index"
        class="list-group-item d-flex justify-content-between align-items-center"
      >
        <div>
          <strong>{{ personagem.nome }}</strong> ({{ personagem.raca }}) - Aliança: {{ personagem.alianca }}
        </div>
        <button @click="deletePersonagem(index)" class="btn btn-danger btn-sm">Deletar</button>
      </li>
    </ul>
    <p v-else class="text-center text-white mt-3">Nenhum personagem cadastrado ainda.</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      novoPersonagem: {
        nome: '',
        raca: '',
        alianca: ''
      },
      personagens: []
    };
  },
  methods: {
    addPersonagem() {
      if (this.novoPersonagem.nome && this.novoPersonagem.raca && this.novoPersonagem.alianca) {
        this.personagens.push({ ...this.novoPersonagem });
        this.novoPersonagem.nome = '';
        this.novoPersonagem.raca = '';
        this.novoPersonagem.alianca = '';
      }
    },
    deletePersonagem(index) {
      this.personagens.splice(index, 1);
    }
  }
};
</script>

<style scoped>
.container {
  max-width: 800px; /* Tamanho do container */
  margin: 0 auto; /* Centraliza o container */
  border-radius: 10px; /* Cantos arredondados */
  background-color: rgba(255, 255, 255, 0.8); /* Fundo semi-transparente */
}
</style>