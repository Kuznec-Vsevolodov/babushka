<template>
    <div class="distribute-block">
        <button @click="distribute" class="btn btn-success">Распределить</button>
        <div v-if="resultVisibility" class="result-container">
            
            <div class="result">
                <h3>Варенья:</h3>

                <div v-for="jam in jams" :key="jam.name">
                    <p>Название: {{jam.name}}</p>
                    <p>Остаток: {{jam.value}}</p>
                    <hr>
                </div>
            </div>

            <div class="result">
                <h3>Банки:</h3>
                <div v-for="bank in banks" :key="bank.name">
                    <p>Номер банки: {{bank.name}}</p>
                    <p>Варенье в банке: {{bank.jamType}}</p>
                    <p>Заполненность: {{bank.fullness}}/{{bank.value}}</p>
                    <hr>
                </div>
            </div>
        </div>
        <div v-if="errorVisibility" style="margin-top: 10px">
            <h3 style="color: #ff0000">Возникла ошибка. Возможно, данные пусты</h3>
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
      emptyBanks: [],
      errorVisibility: false,
      currentBank: []
    }
  }, 
  methods:{
      distribute(){
          try{
                this.jams = JSON.parse(localStorage["Jams"])
                this.banks = JSON.parse(localStorage["Banks"])
                
                this.emptyBanks = this.banks.filter((bank) => {
                    return bank.jamType === '';
                }); 

                console.log(this.emptyBanks);

                this.jams.forEach(jam => {
                    this.banks.forEach(bank => {
                        if(jam.value > 0){
                            if (this.emptyBanks.includes(bank) && bank.value/2 < jam.value || bank.jamType == jam.name){
                                this.putJamToBank(bank, jam)
                                this.cleanEmptyBanks(bank)
                            }else{
                                var bankIndex = this.banks.indexOf(this.emptyBanks[
                                        this.emptyBanks.length - 1
                                    ]);
                                bank = this.banks[bankIndex]
                                this.putJamToBank(bank, jam)
                                this.cleanEmptyBanks(bank)
                                this.banks[bankIndex] = this.currentBank;
                            }
                        }else{
                            console.log("Варенье кончилось")  
                        }  
                    });
                })
                this.closeError();
                this.showResult();
            }catch(err){
                console.log(err);
                this.showError();
            }
      },
      showResult(){
          this.resultVisibility = true;
      },
      showError(){
          this.resultVisibility = false;
          this.errorVisibility = true;
      },
      closeError(){
          this.errorVisibility = false;
      },
      putJamToBank(bank, jam){
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
         this.currentBank = bank
      },
      cleanEmptyBanks(bank){
         var i = this.emptyBanks.indexOf(bank);
         if(i >= 0) {
            this.emptyBanks.splice(i,1);
         }
      }
  }
}

</script>