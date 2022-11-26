<template>
	<div class="notes">
		<div 
			class="notes__note"
			v-for="(note, index) in notes"
			:key="index"
			:class="{
				column: !gridCards,
				'low': note.priority === 'low',
				'medium': note.priority === 'medium',
				'high': note.priority === 'high'
			}"
		>
			<div class="notes__note-head">
				<h2>{{ note.title }}</h2>
				<p class="notes__note-head-remove" @click="removeNote(index)"></p>
			</div>
			<div class="notes__note-body">
				<p>{{ note.descr }}</p>
			</div>
			<div class="notes__note-date">
				<p>{{ note.date }}</p>
				<svg class="icons">
					<use xlink:href="@/icons/sprite.svg#editIcon"></use>
				</svg>
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
		},
		gridCards: {
			type: Boolean,
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
	flex-flow: wrap;
	padding: 40px 0;
	gap: 20px;
	
	&__note {
		display: flex;
    flex-flow: column;
		padding: 20px;
		background: #fff;
		flex: 0 0 calc(50% - 10px);
		border-radius: 10px;
		transition: all .3s ease;
		&.column {
			flex-basis: 100%;
			transition: all .3s ease;
		}
	}
	&__note-head {
		font-weight: 700;
		font-size: 20px;
		color: #494ce8;
		margin-bottom: 20px;
		position: relative;
		padding-right: 20px;
	}
	&__note-head-remove {
		position: absolute;
		top: 3px;
		right: 0;
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
		flex: 1;
		&>p {
			margin-bottom: 20px;
		}
	}

	&__note-date {
		display: flex;
		justify-content: space-between;
		align-items: center;
		&>p {
			font-size: 14px;
			color: #999;
		}
		&>svg {
			fill: #999;
			cursor: pointer;
		}
	}
}
.low, .medium, .high {
	border-left: 5px solid #26de81;
}
.medium {
	border-color: #fed330;
}
.high {
	border-color: #fc5c65;
}
</style>