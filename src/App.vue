<template>
  <div>
    <banks-init></banks-init>
    <jams-init></jams-init>
    <distribute></distribute>  
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
.creation-div{
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}
input{
  border: 1px solid #000;
  border-radius: 50px;
  height: 30px;
  width: 400px;
  margin-bottom: 20px;
  padding-left: 15px;
}

.buttons{
  display: flex;
  justify-content: space-between;
}

button{
  border: 1px solid #000;
  border-radius: 50px;
  height: 30px;
}

.distribute-block{
  margin-top: 30px;
}
</style>
