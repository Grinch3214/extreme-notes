<template>
  <div class="wrapper">

    <div class="wrapper-content">
      <section class="note">
        <div class="container">
					<div class="note__header">
						<h1 class="note__title">{{ title }}</h1>
					</div>
					<message-vue v-if="message" :message="message" />
					<new-note
						:note="note"
						@addNewNote="addNote"
					/>

						<div class="note__filter">

							<search-vue
								:value="search"
								placeholder="Find note"
								@search="search = $event"
							/>

							<div class="note__icons">
								<svg class="icons" :class="{ active: gridCards }" @click="gridCards = true">
									<use xlink:href="@/icons/sprite.svg#columnIcon"></use>
								</svg>
								<svg class="icons" :class="{ active: !gridCards }" @click="gridCards = false">
									<use xlink:href="@/icons/sprite.svg#gridIcon"></use>
								</svg>
							</div>
						</div>

					<notes-vue :notes="notesFilter" :gridCards="gridCards" @removeItem="removeNote" />
				</div>
      </section>
    </div>

  </div>
</template>

<script>
import MessageVue from "./components/MessageVue.vue";
import NewNote from './components/NewNote.vue';
import NotesVue from './components/NotesVue.vue';
import SearchVue from './components/SearchVue.vue';

export default {
  name: 'App',
  components: {
		MessageVue,
    NewNote,
    NotesVue,
    SearchVue,
  },
	data:() => ({
		title: 'Extreme notes',
		search: '',
		gridCards: true,
		message: null,
		note: {
			title: '',
			descr: '',
			priority: 'low'
		},
		notes: [
			{
				title: 'First note',
				descr: 'Description for first note',
				date: new Date(Date.now()).toLocaleString(),
				priority: 'low'
			},
			{
				title: 'Second note',
				descr: 'Description for second note',
				date: new Date(Date.now()).toLocaleString(),
				priority: 'medium'
			},
			{
				title: 'Last note',
				descr: 'Description for last note',
				date: new Date(Date.now()).toLocaleString(),
				priority: 'high'
			},
		],
		priorities: [
			{ title: 'low' },
			{ title: 'medium' },
			{ title: 'high' }
		]
	}),
	computed: {
		notesFilter() {
			let arr = this.notes;
			let search = this.search;

			if (!search) return arr;

			search = search.trim().toLowerCase();

			arr = arr.filter((item) => {
				if (item.title.toLowerCase().indexOf(search) !== -1) {
					return item
				}
			})
			return arr;
		}
	},
	methods: {
		addNote() {
			let { title, descr, priority } = this.note;

			if (title === '') {
				this.message = 'Title can`t be blank'
				return false
			}

			this.notes.push({
				title,
				descr,
				priority,
				date: new Date(Date.now()).toLocaleString()
			});

			this.message = null;
			this.note.title = '',
			this.note.descr = '',
			this.note.priority = 'low'
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

	&__filter {
		display: flex;
		justify-content: space-between;
		align-items: center;
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
