<template>
  <v-card v-bind="$attrs" :style="styles" v-on="$listeners">
    <offset
      v-if="hasOffset"
      :inline="inline"
      :full-width="fullWidth"
      :offset="offset"
    >
      <v-card
        v-if="!$slots.offset"
        color="blue lighten-3"
        elevation
        class="pa-1"
        dark
        width="180px"
        style="border-radius: 30px"
      >
        <slot v-if="!title && !text" name="header" />
        <span v-else>
          <p class="headline text-center mt-2 mb-1" v-text="title" />
        </span>
      </v-card>
      <slot v-else name="offset" />
    </offset>

    <v-card-text>
      <slot />
    </v-card-text>

    <v-divider v-if="$slots.actions" class="mx-3" />

    <v-card-actions v-if="$slots.actions">
      <slot name="actions" />
    </v-card-actions>
  </v-card>
</template>

<script>
import Offset from "@/components/Offset";
export default {
  components: {
    Offset
  },
  inheritAttrs: false,

  props: {
    elevation: {
      type: [Number, String],
      default: 10
    },
    inline: {
      type: Boolean,
      default: false
    },
    fullWidth: {
      type: Boolean,
      default: false
    },
    offset: {
      type: [Number, String],
      default: 24
    },
    title: {
      type: String,
      default: undefined
    }
  },

  computed: {
    hasOffset() {
      return (
        this.$slots.header || this.$slots.offset || this.title || this.text
      );
    },
    styles() {
      if (!this.hasOffset) return null;

      return {
        marginBottom: `${this.offset}px`,
        marginTop: `${this.offset}px`
      };
    }
  }
};
</script>
