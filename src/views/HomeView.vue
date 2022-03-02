<template>
	<h1>REACTION GAME</h1>
	Press play to test your reaction time, click on the box below as soon as it
	gets colored.
	<button @click="handleClick" :disabled="isPlaying">> Play</button>
	<ReactionTester
		v-if="isPlaying"
		:delay="delay"
		@gameOver="handleGameOver"
	></ReactionTester>
	<p v-if="!isPlaying && reactionTime != null">
		Your reaction time is <strong>{{ reactionTime }}</strong>
	</p>
</template>

<script lang="ts">
import { defineComponent } from "vue"
import ReactionTester from "../components/ReactionTester.vue"

type data = {
	delay: null | number
	isPlaying: boolean
	reactionTime: null | number
}

export default defineComponent({
	name: "HomeView",
	components: { ReactionTester },
	data: (): data => ({
		delay: null,
		isPlaying: false,
		reactionTime: null
	}),
	methods: {
		handleClick() {
			this.reactionTime = null
			this.delay = 1000 + Math.random() * 2000
			this.isPlaying = true
		},
		handleGameOver(reactionTime: number) {
			this.reactionTime = reactionTime
			this.isPlaying = false
		}
	}
})
</script>

<style scoped>
button {
	display: block;
	margin: 1rem 0;
}
</style>
