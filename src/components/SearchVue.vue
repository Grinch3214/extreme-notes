<template>
  <div class="search-wrapper">

    <!-- Search -->
    <div class="search-wrapper__icon">
      <div class="search-wrapper__icon-ico">
				<svg class="icons">
					<use xlink:href="@/icons/sprite.svg#searchIcon"></use>
				</svg>
			</div>
    </div>
    <!-- Search input -->
    <input class="search-wrapper__input" type="text" :placeholder="placeholder" v-model="search"/>

  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      required: true
    },
    placeholder: {
      type: String,
      default: 'Search'
    }
  },
  data () {
    return { search: this.value }
  },
  watch: {
    search (val) {
      // console.log(val)
      this.$emit('search', val);
    }
  }
}
</script>

<style lang="scss" scoped>
svg {
  color: #e4e4e4;
}
/* Search-wrapper */
.search-wrapper {
  position: relative;

	&__icon {
		top: 0px;
		bottom: 0px;
		left: 0px;
		position: absolute;
	}

	&__icon-ico {
		height: 100%;
		padding-left: 16px;
		padding-right: 16px;
		align-items: center;
		display: flex;
		.icons {
			stroke: #e4e4e4;
		}
	}

	&__input {
		padding: 16px 16px 16px 56px;
		margin-bottom: 0px;
		border-radius: 30px;
		color: #909399;
		font-size: 16px;
		min-width: 400px;
		height: auto;
	}
}
</style>


