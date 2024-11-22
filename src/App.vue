<script>
  export default{
    name:"App",
    data(){
      return{
        weight:null,   //accepts the weight in kg
        height:null,  //accepts the height in cm
        bmi:null,  // calculates the bmi on the basis of weight and height entered. 
      }
    },
    computed:{
      bmiCategory(){
        if (!this.bmi) return " ";
        if (this.bmi < 18.5) return "Underweight";
        if (this.bmi >= 18.5 && this.bmi < 24.9) return "Normal";
        if (this.bmi >=24.9 && this.bmi < 29.9) return "Overweight";
        return "Obesity";
      } //created a computed property to determine whether a person is underweight, normal or overweight.

    },
    methods:{
      calculate(){
        if(this.weight && this.height){
          const h = this.height / 100; //converting the height into meters
          this.bmi = this.weight / (h * h);  
        }else{
          this.bmi = null;   //if no input then the bmi output will be empty
        }
      },
      reset(){
        this.weight = " ",
        this.height = " ",
        this.bmi=" "
      }
    }
  }

</script>

<template>
<div class="calculator">
  <h1>BMI Calculator</h1>

  <!-- Weight input -->
  <div class="input-grp">
    <label for="weight">Weight (kg):</label>
    <input type="number" placeholder="Enter your weight" v-model="weight" />
  </div>

  <!-- Height input -->
  <div class="input-grp">
    <label for="height">Height (cm):</label>
    <input type="number" placeholder="Enter your height" v-model="height" />
  </div>

  <!-- Button group to calculate and reset the BMI -->
  <div class="btn-grp">
    <button @click="calculate">Calculate BMI</button>
    <button @click="reset">Reset</button>
  </div>

  <!-- Display BMI and category if values are valid -->
  <div v-if="bmi" class="result">
    <p>BMI Calculated is: {{ bmi }}</p>
    <p>{{ bmiCategory }}</p>
  </div>
</div>
</template>

<style>
  .calculator{
    background-color:rgb(30, 37, 74);
    margin:10px 0;
    padding:20px;
    border:1px solid white;
    border-radius:5px;
    width:100%;
  }
  .input-grp{
    margin:20px 0;
    display:flex;
    flex-direction: column;
    text-align: left;
  }

  input{
    padding:10px;
    margin-top:5px;
    border-radius:5px;
    border:1px;
    width: 100%;
  }

  .btn-grp{
    margin:20px 0;
    display:flex;
    justify-content: center;
    padding: 5px;
  }

  button{
    padding:8px 8px;
    margin: 10px;
    background-color: rgb(38, 38, 143);
    color:white;
    border:1px solid white;
    border-radius:3px;
    cursor:pointer;
  }

  button:hover{
    background-color: blue;
  }

  .result{
    margin-top:20px;
    color:white;
  }

  h1{
    color:black;
    font-weight: 600;
    font-size:large;
    text-decoration: underline;
    text-align: center;
  }
</style>
