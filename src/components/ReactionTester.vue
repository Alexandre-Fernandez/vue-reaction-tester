<template>
	<div class="reaction-tester">
		<div v-if="isShown" class="colored-div" @click="handleClick"></div>
	</div>
</template>

<script lang="ts">
import { defineComponent } from "vue"

type data = {
	timer: null | number
	reactionTime: null | number
	isShown: boolean
	initialTime: number
}

export default defineComponent({
	data: (): data => ({
		timer: null,
		initialTime: 0,
		reactionTime: null,
		isShown: false
	}),
	props: ["delay"],
	methods: {
		handleClick() {
			this.reactionTime = Date.now() - this.initialTime
			this.$emit("gameOver", this.reactionTime)
		}
	},
	mounted() {
		this.initialTime = Date.now() + this.delay
		this.timer = setTimeout(() => {
			this.isShown = true
			if (this.timer) clearTimeout(this.timer)
		}, this.delay)
	}
})
</script>

<style scoped>
.reaction-tester {
	margin-top: 1rem;
	width: 25rem;
	height: 25rem;
	border: 1px solid black;
	display: flex;
	align-items: center;
	justify-content: center;
}

.colored-div {
	width: 100%;
	height: 100%;
	background-color: red;
}
</style>
