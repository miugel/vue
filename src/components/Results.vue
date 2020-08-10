<template>
	<div class="results-container">
		<h2>Results</h2>
		<p class="questions-correct">You got {{ correctlyAnswered }}/{{ currentSelections.length }} questions correct</p>
		<p class="percentage">{{ ((correctlyAnswered / currentSelections.length) * 100).toFixed(2) }}%</p>
	</div>
</template>

<script>
	export default {
		name: "Results",
		props: {
			questions: Object,
			currentSelections: Array
		},
		data: () => ({
			// Keep track of correctly answered questions
			correctlyAnswered: 0
		}),
		mounted() {
			// Iterate over questions and compare correct question to currently selected and calculate, rounding?
			this.questions.questions.map((question, index) => {
				if (question.correct_answer === question.choices[this.currentSelections[index]]) {
					this.correctlyAnswered += 1;
				}
			});
		}
	};
</script>

<style>
	.results-container {
		align-items: center;
		display: flex;
		flex-direction: column;
		margin-bottom: 24px;
	}

	h2 {
		color: #2c3e50;
		font-size: 20px;
		margin-bottom: 8px;
		text-decoration: underline;
	}

	.questions-correct {
		color: #2c3e50;
		margin-bottom: 3px;
		font-size: 18px;
		font-weight: 600;
	}

	.percentage {
		color: #dd4b39;
		font-size: 18px;
		font-weight: 600;
	}
</style>