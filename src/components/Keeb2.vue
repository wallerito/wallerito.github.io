<template>
  <div class="keeb-wrapper">
    le keeb &#9;
    <div
    :class="`${selectedKeeb}`"
    class="keeb" 
    ref="keeb">
        <component
          v-for="key in currentKeeb"
          :is="rowComponent(key.type)"
          :key="key.id"
          :keyId="key.id"
          :units="key.units"
          :type="key.type"
          :legend="key.legend"
          :span="key.span"
          :margin-top="key.marginTop"
          :margin-right="key.marginRight"
          :margin-bottom="key.marginBottom"
          :margin-left="key.marginLeft"
          :border-top="key.borderTop"
          :border-bottom="key.borderBottom"
          :radius-top-left="key.radiusTopLeft"
          :radius-top-right="key.radiusTopRight"
          :radius-bottom-left="key.radiusBottomLeft"
          :radius-bottom-right="key.radiusBottomRight"
          :top="key.top"
          :right="key.right"
          :bottom="key.bottom"
          :left="key.left"
          :mid="key.mid"
          :selected-keys="selectedKeys"
          @clicked="toggleSelectedKey($event)"/>
    </div>
    <v-select
      v-model="selectedKeeb"
      :items="keebs"
      label="Keeb"
      outlined
      @change="changeKeyboard($event)"/>
    <v-select
      v-model="currentUpdate"
      :items="updateItems"
      label="Update"
      outlined/>
    <v-color-picker 
      v-model="color"
      :mode="'hexa'"
      :show-swatches="true"
      :swatches="swatches"
      @input="updateColor($event)"
    />
  </div>
</template>

<script>
import Key from './Key.vue'
import KeyGap from './KeyGap.vue'
import va69 from '../resources/va69.js'
import va88 from '../resources/va88.js'
  // 71 cols (17x4 + 1(gap) +2(case))
export default {
  name: 'Keeb',
  components: {
      Key,
      KeyGap,
  },
  data() {
    return {
      VA69: va69,
      VA88: va88,
      keebs: ['VA69', 'VA88'],
      selectedKeeb: 'VA88',
      currentKeeb: {},
      selectedKeys: [],
      currentUpdate: 'All',
      updateItems: [
        'All',
        'Alphanumeric',
        'Modifiers',
        'Selected Keys',
        'Case',
        'Backplate',
      ],
      color: '#ffffff',
      swatches: [
        [
          '#d65030', 
          '#eaece7',
          '#d3d2ce',
          '#57c4ca',
          '#f4c75f',
          '#f48a2d',
          '#4888d0',
          '#69bd4d'
        ],
      ],
    }
  },
  mounted() {
    this.currentKeeb = this.VA88;
  },
  methods: {
    rowComponent(type) {
      return type !== 'gap' ? 'Key' : 'KeyGap';
    },
    changeKeyboard(keyboard){
      this.currentKeeb = this[keyboard];
    },
    toggleSelectedKey(key) {
      const toggle = (k) => {
        const index = this.selectedKeys.indexOf(k);
        if (index !== -1) {
          this.selectedKeys.splice(index, 1);
        } else {
          this.selectedKeys.push(k);
        }
      }
      toggle(key);
      if(key === 'return') {
        toggle('return-small');
      } else if (key === 'return-small') {
        toggle('return');
      }
    },
    updateColor(color) {
      console.log(color);
      console.log(this.$refs.keeb)
      switch(this.currentUpdate) {
        case 'All':
          this.$refs.keeb.style.setProperty('--modifier-color', color);
          this.$refs.keeb.style.setProperty('--alpha-color', color);
          break;
        case 'Modifiers':
          this.$refs.keeb.style.setProperty('--modifier-color', color);
           break;
        case 'Alphanumeric':
          this.$refs.keeb.style.setProperty('--alpha-color', color);
           break;
        case 'Case':
          this.$refs.keeb.style.setProperty('--case-color', color);
           break;
        case 'Backplate':
          this.$refs.keeb.style.setProperty('--backplate-color', color);
           break;
        case 'Selected Keys': 
          if (this.selectedKeys.length) {
            this.selectedKeys.map((key) => {
              this.$refs.keeb.style.setProperty(`--${key}-color`, color);
            })
          }
          break;
        default:
          return;
      }
    }
  },
}
</script>

<style lang="scss">

  .keeb-wrapper {
    padding: 2rem;
  }

  .keeb {
    margin: 3rem;
    box-sizing: content-box;
    display: grid;
    grid-template-columns: repeat(75 , 1.5rem);
    width: fit-content;
    border-radius: 1rem;
    --backplate-color: #000;
    --case-color: #353535;
    --alpha-color: #ECEEE9;
    --modifier-color: #D4D3CC;
    --modifier-color: rgb(184, 183, 175);
    background-color: var(--backplate-color);
  }
  .VA69 {
    grid-template-columns: repeat(71 , 1.5rem);
  }
  .VA88 {
    grid-template-columns: repeat(75 , 1.5rem);
  }

  #return {
    grid-row: auto / span 2;
    height: calc(100% - 2rem);
    border-top-left-radius: 0;
    display: flex;
    align-items: center;
    .key__top {
      height: calc(100% - 0.2rem);
      border-top-left-radius: 0;
      clip:rect(10px 10px 10px 10px);
      // box-shadow: none;
    }
  }
  #return-small {
    position: relative;
    padding-left: 0;
    padding-right: 0;
    margin-right: -1rem;
    box-shadow: 
    inset 10px 10px 10px -6.5px rgba(0,0,0,0.39),
    inset 0px -10px 5px -6.5px rgba(0,0,0,0.1);
    z-index: 5;
    &::before {
      content: '';
      position: absolute;
      left: 10px;
      width: 68px;
      height: 38px;
      background-color: var(--return-color, var(--modifier-color));
      border-top-left-radius: 0.8rem;
      border-top-right-radius: 0.8rem;
      border-bottom-left-radius: 0.8rem;
      background: radial-gradient(ellipse at center,var(--return-color, var(--modifier-color)) 50%, transparent);
      filter: contrast(110%);
      z-index: 900000;
    }
    .key__top {
      // box-shadow: none;
      
      border-right: none;
      position: absolute;
      // margin-right: -10px;
      border-top-right-radius: 0;
      border-bottom-right-radius: 0;
      // margin-right: -10px;
      left: 9px;
      width: 1.5rem;
      z-index: 9;
    }
  }

  .keeb__key--return-small {
   grid-column: span 1;
   border-top-right-radius: 0;
   border-bottom-right-radius: 0;
   margin-right: -10px;
   /* margin-bottom: -5px; */
   z-index: 5;
   filter: none;
    box-shadow: 
    inset 10px 10px 10px -6.1px rgba(0,0,0,0.4),
    inset 0px -10px 5px -6.5px rgba(0,0,0,0.1);
      /* inset 40px -10px 10px -25px rgba(0,0,0,0.33); */
  }
  .keeb__key--return-small::before {
    /* filter: none !important; */
    width: 15px;
    height: 38px;
    z-index: 100;
    border-right: none;
    box-shadow: none;
    border-top-right-radius: 0;
    border-bottom-right-radius: 0;
  }

  .v-color-picker__edit * {
    font-size: 1.5rem !important;
  }
</style>