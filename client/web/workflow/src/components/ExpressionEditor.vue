<template>
  <div
    class="position-relative"
  >
    <c-ace-editor
      v-model="expressionValue"
      :lang="lang"
      :height="height"
      :show-line-numbers="showLineNumbers"
      :font-size="fontSize"
      :show-popout="showPopout"
      auto-complete
      :border="border"
      :auto-complete-suggestions="expressionAutoCompleteValues"
      v-on="$listeners"
    />
  </div>
</template>

<script>
import { components } from '@cortezaproject/corteza-vue'
import { EXPRESSION_EDITOR_AUTO_COMPLETE_VALUES } from '../lib/editor-auto-complete.js'

const { CAceEditor } = components

export default {
  components: {
    CAceEditor,
  },

  props: {
    value: {
      type: String,
      default: '',
    },

    lang: {
      type: String,
      default: 'text',
    },

    height: {
      type: String,
      default: '80',
    },

    showLineNumbers: {
      type: Boolean,
      default: false,
    },

    fontSize: {
      type: String,
      default: '14px',
    },

    border: {
      type: Boolean,
      default: true,
    },

    showPopout: {
      type: Boolean,
      default: true,
    },
  },

  data () {
    return {
      expressionAutoCompleteValues: EXPRESSION_EDITOR_AUTO_COMPLETE_VALUES,
    }
  },

  computed: {
    expressionValue: {
      get () {
        return this.value
      },

      set (value = '') {
        this.$emit('update:value', value)
      },
    },
  },
}
</script>

<style lang="scss" scoped>
.popout {
  z-index: 7;
  bottom: 0;
  right: 0;
}
</style>
