<template>
    <div class="distribute-block">
        <button @click="distribute">Распределить</button>
        <div v-if="resultVisibility">
            
            <h2>Варенья:</h2>

            <div v-for="jam in jams" :key="jam.name">
                <p>Название: {{jam.name}}</p>
                <p>Остаток: {{jam.value}}</p>
                <hr>
            </div>

            <h2>Банки:</h2>
            <div v-for="bank in banks" :key="bank.name">
                <p>Номер банки: {{bank.name}}</p>
                <p>Варенье в банке: {{bank.jamType}}</p>
                <p>Заполненность: {{bank.fullness}}/{{bank.value}}</p>
                <hr>
            </div>
        </div>
        <div v-if="errorVisibility">
            <h2 style="color: #ff0000">Возникла ошибка. Возможно, данные пусты</h2>
        </div>
    </div>
</template>

<script>
export default {
  data(){
    return{
      jams: [],
      banks: [],
      resultVisibility: false,
      errorVisibility: false
    }
  }, 
  methods:{
      distribute(){
          try{
                this.jams = JSON.parse(localStorage["Jams"])
                this.banks = JSON.parse(localStorage["Banks"])
                
                this.jams.forEach(jam => {
                    this.banks.forEach(bank => {
                        if(jam.value > 0){
                        if (bank.jamType == ''){
                            bank.jamType = jam.name;
                            if (bank.value < jam.value){
                                bank.fullness = bank.value;
                                jam.value = jam.value - bank.value;
                                console.log(jam)
                                console.log (bank)
                            }else{
                                bank.fullness = jam.value
                                jam.value = 0;
                                console.log (bank)
                            }
                            }
                        }else{
                            console.log("Варенье кончилось")  
                        }  
                    });
                })
                this.closeError();
                this.showResult();
            }catch{
                this.showError();
            }
      },
      showResult(){
          this.resultVisibility = true;
      },
      showError(){
          this.errorVisibility = true;
      },
      closeError(){
          this.errorVisibility = false;
      }
  }
}

</script>