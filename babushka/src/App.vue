<template>
  <div>
    <div class="container main-conteiner">
      <div class="creation-container">  
        <banks-init></banks-init>
        <jams-init></jams-init>
      </div>
      <hr>
      <distribute></distribute>
    </div>
  </div>
</template>

<script>
import BanksInit from '@/components/BanksInitComponent'
import JamsInit from '@/components/JamInitComponent'
import Distribute from '@/components/DistributeComponent'

export default {
  name: 'App',
  components: {
    BanksInit,
    JamsInit,
    Distribute
  },
  mounted(){
     localStorage["Jams"] = null;          
     localStorage["Banks"] = null;          
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
}

.main-conteiner{
  padding-left: 100px !important;
  padding-right: 100px !important;
  margin-top: 20px;
}

.creation-container{
  display: flex;
  justify-content: space-between;
}

.creation-div{
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}
.form-input{
  border: 1px solid #000 !important;
  border-radius: 50px !important;
  height: 30px !important;
  width: 400px !important;
  margin-bottom: 20px;
  padding-left: 15px;
}

.buttons{
  display: flex;
  justify-content: space-between;
  width: 100%;
}

button{
  border: 1px solid #000;
  border-radius: 50px !important;
  height: 30px;
  line-height: 10px !important;
}

.creation-div{
  width: 400px;
}

.bank-error{
  margin-top: 15px;
  margin-bottom: 0px;
  color: red;
  font-weight: bold;
}

.distribute-block{
  margin-top: 15px;
}

.result-container{
  display: flex;
}

.result{
  width: 50%;
  padding: 15px;
}

</style>
