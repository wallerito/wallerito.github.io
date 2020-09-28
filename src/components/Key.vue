<template>
  <div class="key" :id="keyId" ref="key"
  :class="[`key--${units}`, `key--${type}`, selected ? 'key--selected' : '']"
  @click="$emit('clicked', keyId)">
    <div class="key__top">
      <slot>
        <div 
          v-if="Array.isArray(legend)"
          class="key__top__legend key__top__legend--double">
          <span> {{ legend[0] }}</span>
          <span> {{ legend[1] }}</span>
        </div>
        <span 
          v-else 
          class="key__top__legend">
          {{ legend }}
        </span>
      </slot>
    </div>
  </div>
</template>
<script>
export default {
  name: 'Key',
  props: {
    keyId: {
        type: String,
        required: true,
    },
    units: {
        type: String,
        required: false,
        default: '1',
    },
    type: {
        type: String,
        required: false,
        default: 'alpha',
    },
    legend: {
        type: [String, Array],
        required: false,
        default: '',
    },
    selectedKeys: {
      type: Array,
      required: false,
      default: () => [],
    }
  },
  computed: {
    selected() {
      return this.selectedKeys.includes(this.keyId);
    },
  },
  mounted() {
    this.$refs.key.style.setProperty('background-color', `var(--${this.keyId}-color, var(--${this.type}-color))`);
  },
}
</script>
<style lang="scss" scoped>

  .key {
    font-family: Arial, sans-serif;
    margin: 0.1rem;
    padding: 0.9rem;
    height: 4rem;
    background-color: var(--alpha-color);
    border-radius: 0.3rem;
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: inset 0 0 1rem 0.3rem rgba(0,0,0,0.4);
    // filter: drop-shadow(0 3px 5px rgba(255, 255, 255, 0.7));
    &.key--selected {
      outline: 2px solid red;
    }
    &.key--1 {
      grid-column: span 4;
    }
    &.key--1-25 {
      grid-column: span 5;
    }
    &.key--1-5 {
      grid-column: span 6;
    }
    &.key--1-75 {
      grid-column: span 7;
    }
    &.key--2 {
      grid-column: span 8;
    }
    &.key--2-75 {
      grid-column: span 11;
    }
    &.key--6-25 {
      grid-column: span 25;
    }
    &.key--alpha {
      font-size: 2rem;
    }
    &.key--modifier {
      font-size: 1rem;
      font-weight: 600;
    }

    .key__top {
      text-transform: uppercase;
      display: flex;
      align-items: center;
      justify-content: center;
      width: 100%;
      height: 3.8rem;
      background-color: inherit;
      border: 0.1rem solid rgba(255, 255, 255, 0.05);
      box-shadow: inset 0 0 0.5rem 0.3rem rgba(0,0,0,0.05);
      filter: contrast(110%);
      border-radius: 0.8rem;
      .key__top__legend {
        opacity: 0.8;
        white-space: pre-line;
      }
      .key__top__legend--double {
        height: 100%;
        display: flex;
        flex-direction: column;
        // align-items: space-between;
        justify-content: space-around;
        font-size: 1.3rem;
      }
    }
  }

</style>
