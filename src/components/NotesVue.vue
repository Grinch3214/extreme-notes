<template>
	<div class="notes">
		<div class="notes__note" v-for="(note, index) in notes" :key="index">
			<div class="notes__note-head">
				<h2>{{ note.title }}</h2>
				<p class="notes__note-head-remove" @click="removeNote(index)"></p>
			</div>
			<div class="notes__note-body">
				<p>{{ note.descr }}</p>
				<span>{{ note.date }}</span>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	props: {
		notes: {
			type: Array,
			default: []
		}
	},
	methods: {
		removeNote(index) {
			this.$emit('removeItem', index);
		}
	}
}
</script>

<style lang="scss">
.notes {
	display: flex;
	align-items: center;
	flex-flow: wrap;
	padding: 40px 0;
	gap: 20px;
	
	&__note {
		padding: 20px;
		background: #fff;
		flex: 0 0 calc(50% - 10px);
		border-radius: 10px;
	}
	&__note-head {
		font-weight: 700;
		font-size: 20px;
		color: #494ce8;
		margin-bottom: 20px;
		text-transform: uppercase;
		position: relative;
	}
	&__note-head-remove {
		position: absolute;
		top: 15px;
		right: 15px;
		width: 15px;
		height: 15px;
		cursor: pointer;
		&::before,
		&::after {
			content: '';
			position:absolute;
			top: 6px;
			left: 0;
			right: 0;
			height: 2px;
			background: #494ce8;
			transform: rotate(45deg);
		}
		&::after {
			transform: rotate(-45deg);
		}
	}
	&__note-body {
		&>p {
			margin-bottom: 20px;
		}
		&>span {
			font-size: 14px;
			color: #999;
		}
	}
}
</style>