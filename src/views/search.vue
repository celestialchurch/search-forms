<template>
  <div id="main">
    <div id="primary">
      <div class="search">
        <input type="text" placeholder="Pesquisar por nome" @keydown="search()" @click="searchUp()" v-model="searchInput">
        <span class="exit" @click="searchExit">
          <i class="fas fa-times"></i>
        </span>
        <ul id="peoples">
          <li 
          v-for="(element,index) in newDatabase" :key="index" @click="pushData(index)">
            {{element.nome}} | {{element.number}}
          </li>
        </ul>
      </div>
      <br>
      <div class="form">
        <iframe 
        src="https://docs.google.com/forms/d/e/1FAIpQLSeWUfET3LR6g_7puW79VmhZf4PRoCEtmcVXRFgtyNNbu_iFIg/viewform?embedded=true" 
        height="2523" 
        id="frame"
        frameborder="0" 
        marginheight="0" 
        marginwidth="0">Carregando…</iframe>
      </div>
    </div>
  </div>
  
</template>

<script>
import file from '../../database/file.json'
export default {
  name: 'HomeView',
  data(){
    return {
      list: this.funnel(file),
      searchInput: '',
      newDatabase: this.funnel(file)
    }
  },
  methods: {
    funnel(datas){
      return datas
    },
    searchUp(){
      document.getElementById('peoples').classList.add('active')
    },
    searchExit(){
      document.getElementById('peoples').classList.remove('active')
    },
    pushData(index){
      var list = this.list[index]
      var url = `https://docs.google.com/forms/d/e/1FAIpQLSeWUfET3LR6g_7puW79VmhZf4PRoCEtmcVXRFgtyNNbu_iFIg/viewform?usp=pp_url&entry.456931737=${list.nome}&entry.96761479=${list.regiao}&entry.773359901=${list.number}&entry.1172068566=${list.igreja}&entry.2125757515=${list.cidade}&entry.292054885=${list.convite}&entry.930101984=Mais+vezes&entry.400014742=${list.faixa}&entry.725629179=${list.sexo}`
      window.open(url,'_blank')
    },
    search(){
      if(this.searchInput !== ''){
        this.newDatabase = 
        this.list.filter(searchs => searchs.nome.includes(this.searchInput))
      }
      else{
        this.newDatabase = this.list
      }
    }
  },
}
</script>


<style scope>
*{
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
.exit{
  padding: 10px 15px;
  margin-right: 10px;
  border-radius: 0px 50px 50px 0px;
  background-color: rgb(62, 202, 6);
  border: solid 2px rgb(62, 202, 6);
  font-size: 15px;
  color: white;
  cursor: pointer;
}
#main{
  display: flex;
}
#primary{
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 20px 0px;
}
#primary .search{
  display: flex;
  position: relative;
  width: 570px;
}
#primary .search input{
  width: 100%;
  padding: 10px;
  border-radius: 50px 0px 0px 50px;
  border: solid 1px rgb(87, 87, 87);
  font-size: 15px;
}
#primary .search button{
  border-radius: 300px;
  background-color: rgb(62, 202, 6);
  border: solid 2px rgb(62, 202, 6);
  color: white;
  padding: 0px 10px;
  font-size: 15px;
}
#primary .search ul{
  position: absolute;
  height: 200px;
  overflow: auto;
  background-color: white;
  width: 97%;
  top: 70%;
  display: none;
  padding: 0px;
  padding-right: 3px;
  border: solid 1px rgb(200, 200, 200);
}
#primary .search ul::-webkit-scrollbar{
  width: 5px;
}
#primary .search ul::-webkit-scrollbar-thumb{
  width: 5px;
  background-color: rgb(200, 200, 200);
  border-radius: 10px;
}
#primary .search ul.active{
  display: block;
}
#primary .search ul li{
  list-style: none;
  padding: 10px;
  border-bottom: solid 1px rgb(235, 235, 235);
  cursor: pointer;
}
#primary .search ul li:hover{
  background-color: rgb(235, 235, 235);
}

.form{
  display: flex;
}
#frame{
  width: 640px;
}
</style>