<template>
  <div>
    <div class="number" :id="'number-'+number" v-for="number in listOfRandomNumbers()" :key="number" @mouseover="highlight(number)" @mouseout="reset" ref="numberRef">
      {{number}}
    </div>
  </div>
</template>

<script>
export default {
  props: {number:Number},
  data()
  {
    return {
      none: null
    }
  },
  methods: {
    listOfRandomNumbers()
    {
      let numbers = [];
      for(var i = 1; i < (this.$props.number + 1); i++)
      {
        numbers = [...numbers, i];
      }
      for (let i = numbers.length -1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [numbers[i], numbers[j]] = [numbers[j], numbers[i]];
      }
      return numbers
    },
    highlight(number)
    {
      const nums = this.$refs.numberRef

      for(let i = 0; i < nums.length; i++)
      {
        const num = nums[i].innerText.trim();
        if(number % num === 0)
        {
          nums[i].classList.add('active')
          console.log('divisor', num)
        }
      }
    },
    reset()
    {
      const nums = document.querySelectorAll('.number');
      nums.forEach(num => num.classList.remove('active'))
    }
  }
}
</script>

<style scoped>
	.number {
		display: inline-block;
		padding: 5px;
		background-color: lightgrey;
		margin: 5px;
	}

	.active {
		background-color: red;
	}
</style>
