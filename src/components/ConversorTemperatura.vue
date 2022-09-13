<template>
  <div>
     <table>
        <tr>
          <th>Celsius</th>
          <th>Fahrenheit</th>
        </tr>
        <tr>
            <tr
          v-for="p in projetosfiltrados"
          :key="p.id"
          @click="selected = p"
          :class="{ selected: isSelected(p) }">
        </tr>
      </table>
  </div>  
</template>

<script>
export default {
    props: {
    c1: 20,
    c2: 60,
  },
  data() {
    return {
      tabela: "",
     mounted() {
        this.projetos.forEach(p => maiorId = p.id > maiorId ? p.id : maiorId)
     }    
  }

 }
}
</script>

<style>

</style>