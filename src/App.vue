<template>
  <div class="wrapper">

    <div class="wrapper-content">
      <section class="note">
        <div class="container">
					<div class="note__header">
						<h1 class="note__title">{{ title }}</h1>
					</div>
					<message-vue v-if="message" :message="message" />
					<new-note :note="note" @addNewNote="addNote" />

						<div class="note__icons">
							<svg class="icons" :class="{ active: gridCards }" @click="gridCards = true">
								<use xlink:href="@/icons/sprite.svg#columnIcon"></use>
							</svg>
							<svg class="icons" :class="{ active: !gridCards }" @click="gridCards = false">
								<use xlink:href="@/icons/sprite.svg#gridIcon"></use>
							</svg>
						</div>

					<notes-vue :notes="notes" :gridCards="gridCards" @removeItem="removeNote" />
				</div>
      </section>
    </div>

  </div>
</template>

<script>
import MessageVue from "./components/MessageVue.vue";
import NewNote from './components/NewNote.vue';
import NotesVue from './components/NotesVue.vue';

export default {
  name: 'App',
  components: {
		MessageVue,
    NewNote,
    NotesVue,
  },
	data:() => ({
		title: 'Extreme notes',
		gridCards: true,
		message: null,
		note: {
			title: '',
			descr: ''
		},
		notes: [
			{
				title: 'First note',
				descr: 'Description for first note',
				date: new Date(Date.now()).toLocaleString()
			},
			{
				title: 'Second note',
				descr: 'Description for second note',
				date: new Date(Date.now()).toLocaleString()
			},
			{
				title: 'Last note',
				descr: 'Description for last note',
				date: new Date(Date.now()).toLocaleString()
			},
		],
	}),
	methods: {
		addNote() {
			let { title, descr } = this.note;

			if (title === '') {
				this.message = 'Title can`t be blank'
				return false
			}

			this.notes.push({
				title,
				descr,
				date: new Date(Date.now()).toLocaleString()
			});

			this.message = null;
			this.note.title = '',
			this.note.descr = ''
		},
		removeNote(index) {
			this.notes.splice(index, 1);
		}
	},
}
</script>

<style lang="scss">
.note {

	&__header {
		text-align: center;
		margin-bottom: 40px;
	}

	&__title {
		font-size: 36px;
		letter-spacing: 2.5px;
	}

	&__icons {
		text-align: right;
		.icons {
			fill: rgba(0,0,0,0);
			stroke: #999999;
			transition: all .3s ease;
			cursor: pointer;
			&.active {
				stroke: #444ce0;
			}
		}
		&>.icons + .icons {
			margin-left: 15px;
		}
	}
}
</style>
