<template>
    <div class="creation-div">
        <h2>Добавление банок</h2>  
        <input v-model="name" type="text" placeholder="Введите номер банки">  
        <input v-model="value" type="number" placeholder="Введите объём банки банки">
        <div class="buttons">
            <button type="submit" @click="createBank">Добавить банку</button>
            <button @click="clearList">Очистить список</button>
        </div>
        
    </div>
</template>

<script>

export default {
  data(){
    return{
      name: '',
      value: 0,
      banks: []  
    }
  }, 
  methods:{
      createBank(){
          var currentBank = {name: this.name, value: this.value, jamType: '', fullness: 0};
          this.banks.push(currentBank);

          localStorage["Banks"] = JSON.stringify(this.banks);          
          console.log(localStorage["Banks"])
      },
      clearList(){
          this.banks = []
          localStorage["Banks"] = JSON.stringify([]);    
          console.log(localStorage["Banks"])
      }
  }
}

</script>