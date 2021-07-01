<template>
    <div class="creation-div">
        <h2>Добавление варенья</h2>  
        <input v-model="name" type="text" placeholder="Название варенья">  
        <input v-model="value" type="number" placeholder="Введите объём варенья">
        <div class="buttons">
            <button type="submit" @click="createJam">Добавить варенье</button>
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
      createJam(){
          if(this.value < 0){
              this.value = -this.value
          }

          var existingJam = this.jams.filter((jam) => {
            return jam.name === this.name.trim();
          });  

          if (existingJam.length > 0){
              var index = this.jams.indexOf(existingJam[0])
              this.jams[index].value += parseInt(this.value);

              localStorage["Jams"] = JSON.stringify(this.jams); 
              console.log(localStorage["Jams"])
          }else{
              var currentJam = {name: this.name.trim(), value: parseInt(this.value)};
              this.jams.push(currentJam);

              localStorage["Jams"] = JSON.stringify(this.jams);          
              console.log(localStorage["Jams"])
          }
          
          this.name = '',
          this.value = ''
      },
      clearList(){
          this.jams = []
          localStorage["Jams"] = JSON.stringify([]);    
          console.log(localStorage["Jams"])
      }
  }
}

</script>