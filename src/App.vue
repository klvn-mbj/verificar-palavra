<template>
  <div id="app">
    
    <div class="container body" data-aos="fade-up" data-aos-duration="1000">
      <div class="jumbotron m-5">
        <h1>Actividade Nº 1</h1>
        <p class="lead">Verificador de caracteres repetidos em uma palavra.</p>
        
        <hr class="my-4">
        
        <div class="form-group">
          <label for="text">Introduza uma palavra</label>
          <input v-model="palavra" type="text" class="form-control" id="text" aria-describedby="text" placeholder="Maria, Banana, Telefone...">
          <small id="emailHelp" class="form-text text-muted">Pode introduzir uma palavra ou uma frase.</small>
        </div>

        <button @click="verificador()"  type="button" class="btn btn-primary">Verificar</button>

        <hr class="my-4">

        <div v-if="func=='x'" class="alert alert-dismissible alert-danger">
          <button type="button" class="close" data-dismiss="alert">&times;</button>
           Não existem caracteres repetidos na palavra <strong>{{n}}</strong>
        </div>

        <ul class="list-group">
          <div v-for="(item, index) in duplicado" :key="item.id">
            <li class="list-group-item d-flex justify-content-between align-items-center">
              {{duplicado[index]}}
              <span class="badge badge-primary badge-pill">{{duplicadoQuant[index]}}</span>
            </li>
          </div>
        </ul>

      </div>
    </div>

  </div>
</template>

<script>

export default {
  name: 'App',

  data() {
    return {
      palavra: '',
      n: '',
      func: '',
      duplicado: [],
      duplicadoQuant: []
    }
  },

  methods: {
    verificador() {

      this.func = '',
      this.duplicado = [];
      this.duplicadoQuant = [];

      if (this.palavra) {

        var sequencia = this.palavra.split("");

        var charTotal=""; var charActual="";

        for(var i=0; i < sequencia.length; i++){

            charActual=sequencia[i].toLowerCase();

            if(charTotal.includes(charActual) && charActual!=" ") {
                
                if(!this.duplicado.includes(charActual)) {

                    this.duplicado.push(charActual);
                    this.duplicadoQuant.push(1);
                    
                } 

                for (var k=0; k < this.duplicado.length; k++){
                    if(this.duplicado[k]===charActual){
                        this.duplicadoQuant[k]+=1;
                    }
                }
            }
            charTotal += charActual;
        }

        document.getElementById("text").classList.remove('is-valid');
        document.getElementById("text").classList.remove('is-invalid');
        
        if(this.duplicado.length > 0) {
          this.func = 1;
          
          document.getElementById("text").classList.add('is-valid');
        } else { this.n=this.palavra; this.func = 'x'; document.getElementById("text").classList.add('is-invalid');}

        this.palavra = "";
      } else {
        document.getElementById("text").classList.add('is-invalid');
      }
    }
  }

}
</script>

<style>
*{
  font-family: 'Poppins', sans-serif;
}
  .body{
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>
