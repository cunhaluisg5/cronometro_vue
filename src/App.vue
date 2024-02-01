<template>
  <div id="app">
    <img src="./assets/cronometro.png" class="img"/>

    <a class="timer">{{numero}}</a>

    <div class="areaBtn">
      <button class="botao" @click="vai">{{botao}}</button>
      <button class="botao" @click="limpar">LIMPAR</button>
    </div>
  </div>
  
  <div class="list" v-show="historico.length > 0">
    <ul>
      <li v-for="item in historico" :key="item">Você fez uma pausa em {{item}}</li>
    </ul>
    <button @click="historico = []">Limpar histórico</button>
  </div>
</template>

<script>
export default {
  name: 'App',
  data(){
    return{
      numero: 0,
      botao: 'VAI',
      timer: null,
      ss: 0,
      mm: 0,
      hh: 0,
      historico: []
    }
  },
  methods:{
    vai(){
      if(this.timer !== null){
        clearInterval(this.timer);
        this.timer = null;
        this.botao = 'VAI';
        if(this.ss !== 0){
          this.historico.push(this.numero);
        }
      }else{
        this.timer = setInterval(() => {
          this.rodarTimer();
        }, 1000);
        this.botao = 'PAUSAR';
      }
    },
    limpar(){
      if(this.timer !== null){
        clearInterval(this.timer);
        this.timer = null;
      }

      this.ss = 0;
      this.mm = 0;
      this.hh = 0;
      this.numero = 0;
      this.botao = 'VAI';
      this.historico = [];
    },
    rodarTimer(){
      this.ss++;

      if(this.ss == 59){
        this.ss = 0;
        this.mm++;
      }

      if(this.mm == 59){
        this.mm = 0;
        this.hh++;
      }

      let format = (this.hh < 10 ? '0'+this.hh : this.hh) + ':'
      + (this.mm < 10 ? '0'+this.mm : this.mm) + ','
      + (this.ss < 10 ? '0'+this.ss : this.ss);

      return this.numero = format;
    }
  }
}
</script>

<style>
  #app{
    display: flex;
    width: 100%;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  }

  .img{
    width: 420px;
    height: 420px;
    padding-top: 100px;
  }

  .timer{
    font-size: 70px;
    margin-top: -210px;
  }

  .areaBtn{
    margin-top: 155px;
    display: flex;
  }

  .botao{
    -webkit-user-select: none;
    -moz-user-select: none;
    width: 150px;
    font-size: 20px;
    border: 0;
    border-radius: 5px;
    text-align: center;
    margin-left: 15px;
    margin-right: 15px;
    padding: 6px;
    cursor: pointer;
  }

  .botao:hover{
    opacity: 0.8;
    transition: all 0.50s;
  }

  ul{
    text-align: center;
    padding: 0px;
  }

  ul li{
    margin-top: 4px;
    padding: 15px;
    background-color: rgb(187, 184, 184);
    list-style: none;
    font-size: 18px;
    border-radius: 6px;
  }

  .list bottom{
    cursor: pointer;
    border: 0;
    padding: 8px;
    border-radius: 5px;
    margin-bottom: 12px;
  }
</style>
