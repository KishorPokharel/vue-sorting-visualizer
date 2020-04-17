<template>
  <div class="array_bars">
	<div class="array_bar_wrapper">
		<div v-for="(h, index) in heights" 
			:key="index" 
			class="each_bar" 
			v-bind:style="{ height: h + 'px' }"
			>
		</div>
	</div>

	<div class="action-buttons">
		<button @click="resetArray" :disabled="comparing">Reset</button>
		<button @click="bubbleSort">Bubble Sort</button>
	</div>
  </div>
</template>

<script>
export default {
	name: 'SortingVisualizer',

	data() {
		return {
			heights: [],
			totalBars: 100,
			i: 0,
			j: 0,
			comparing: false,
		}
	},

	methods: {
		getRandomInt(min, max) {
			min = Math.ceil(min);
			max = Math.floor(max);
			return Math.floor(Math.random() * (max - min + 1)) + min;
		},

		resetArray() {
			this.heights = [];
			for(let i=0; i<this.totalBars; i++) {
				this.heights.push(this.getRandomInt(2, 400));
			}
			this.i = 0;
			this.j = 0;
			return 0;
		},

		bubbleSort() {
			this.comparing = true;
			if(this.i < this.heights.length) {
				for(this.j = 0; this.j<this.heights.length-this.i-1; this.j++) {
					if(this.heights[this.j] > this.heights[this.j+1]) {
						let temp = this.heights[this.j];
						this.$set(this.heights, this.j, this.heights[this.j+1]);
						this.$set(this.heights, this.j+1, temp);
					}
				}
			}else {
				this.comparing = false;
				return 0;
			}
			this.i++;
			setTimeout(this.bubbleSort, 3);
		}
	},

	mounted() {
		for(let i=0; i < this.totalBars; i++) {
			this.heights.push(this.getRandomInt(2, 400));
		}
	},
}
</script>

<style scoped>
.array_bars {
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
}
.array_bar_wrapper {
	width: 800px;
	height: 420px;
	display: flex;
	justify-content: space-between;
}

.each_bar {
	width: 2px;
	background-color: #b0b0b0;
}

.action-buttons {
	display: flex;
	flex-direction: column;
	margin: 20px;
}

.comparing-two {
	background-color: #79bde6;
}
</style>
