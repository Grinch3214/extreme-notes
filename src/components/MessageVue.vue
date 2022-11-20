<template>
	<div class="message">
		<p>{{ message }}</p>
	</div>
</template>

<script>
export default {
	props: {
		message: {
			type: String,
			default: 'default message'
		}
	}
}
</script>

<style lang="scss">
	.message {
		text-align: center;
		padding: 20px;
		color: #fc5c65;
	}
</style>