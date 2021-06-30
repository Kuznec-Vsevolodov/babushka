<template>
    <div class="creation-div">
        <h2>Добавление варенья</h2>  
        <input v-model="name" type="text" placeholder="Название варенья">  
        <input v-model="value" type="number" placeholder="Введите объём варенья">
        <div class="buttons">
            <button type="submit" @click="createBank">Добавить варенье</button>
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
      jams: []  
    }
  }, 
  methods:{
      createBank(){
          var currentJam = {name: this.name, value: this.value};
          this.jams.push(currentJam);

          localStorage["Jams"] = JSON.stringify(this.jams);          
          console.log(localStorage["Jams"])
      },
      clearList(){
          this.jams = []
          localStorage["Jams"] = JSON.stringify([]);    
          console.log(localStorage["Jams"])
      }
  }
}

</script>