<template>
  <ul
    :class="classes"
    class="mdc-image-list">
    <slot/>
  </ul>
</template>

<script>
export default {
  props: {
    standardColumn: {
      type: Number,
      validator: (value) => value >= 1 && value <= 12
    },
    masonryColumn: {
      type: Number,
      validator: (value) => value >= 1 && value <= 12
    },
    textProtection: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    classes () {
      let standard = {}
      if (this.standardColumn > 0 && typeof this.masonryColumn === 'undefined') {
        standard['image-list-standard-' + this.standardColumn] = true
      }

      let masonry = {}
      if (this.masonryColumn > 0 && typeof this.standardColumn === 'undefined') {
        masonry['image-list-masonry-' + this.masonryColumn] = true
        masonry['mdc-image-list--masonry'] = true
      }

      let others = {}
      others['mdc-image-list--with-text-protection'] = this.textProtection

      return {...standard, ...masonry, ...others}
    }
  }
}
</script>
