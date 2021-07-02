<template>
    <div class="creation-div">
        <h2>Добавление банок</h2>  
        <input v-model="name" type="text"  class="form-control form-input" placeholder="Введите номер банки">  
        <input v-model="value" type="number"  class="form-control form-input" placeholder="Введите объём банки банки">
        <div class="buttons">
            <button class="btn btn-primary" type="submit" @click="createBank">Добавить банку</button>
            <button class="btn btn-danger" @click="clearList">Очистить список</button>
        </div>
        <p v-if="errorMessage" class="bank-error">Такая банка уже существует</p>
    </div>
</template>

<script>

export default {
  data(){
    return{
      name: '',
      value: 0,
      banks: [],
      errorMessage: ''
    }
  }, 
  methods:{
      createBank(){
        if(this.value < 0){
            this.value = -this.value
        }

        var existingBank = this.banks.filter((bank) => {
            return bank.name === this.name.trim();
        }); 

        if (existingBank.length > 0){
            this.errorMessage = true
        }else{
            this.errorMessage = false

            var currentBank = {
                name: this.name.trim(), 
                value: parseInt(this.value), 
                jamType: '', 
                fullness: 0
            };
            
            if (this.banks.length > 0 ){
                for (var i = 0; i < this.banks.length; i++){
                    if (this.banks[i].value <= currentBank.value){
                        this.banks.splice(i, 0, currentBank);
                        break;
                    }else if (i == this.banks.length-1){
                        this.banks.push(currentBank);
                        break;
                    }
                }
            }else{
                this.banks.push(currentBank);
            }

            localStorage["Banks"] = JSON.stringify(this.banks);
        }

        this.name = '',
        this.value = ''
      },
      clearList(){
          this.banks = []
          localStorage["Banks"] = null;    
      }
  }
}

</script>