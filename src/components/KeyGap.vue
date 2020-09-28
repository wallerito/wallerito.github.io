<template>
    <div 
      class="keeb__case"
      :class="[
        { 'keeb__case--mt' : marginTop }, 
        { 'keeb__case--mr' : marginRight }, 
        { 'keeb__case--mb' : marginBottom }, 
        { 'keeb__case--ml' : marginLeft }, 
        { 'keeb__case--bt' : borderTop }, 
        { 'keeb__case--bb' : borderBottom }, 
        { 'keeb__case--rtl' : radiusTopLeft }, 
        { 'keeb__case--rtr' : radiusTopRight }, 
        { 'keeb__case--rbl' : radiusBottomLeft }, 
        { 'keeb__case--rbr' : radiusBottomRight }, 
        { 'keeb__case--top' : top }, 
        { 'keeb__case--right' : right }, 
        { 'keeb__case--bottom' : bottom }, 
        { 'keeb__case--left' : left }, 
        { 'keeb__case--mid' : mid }, 
        `keeb__case--span${span}`]"/>
</template>
<script>
export default {
  name: 'Gap',
  props: {
    span: {
        type: Number,
        required: false,
        default: 1,
    },
    marginTop: {
        type: Boolean,
        required: false,
        default: false,
    },
    marginRight: {
        type: Boolean,
        required: false,
        default: false,
    },
    marginBottom: {
        type: Boolean,
        required: false,
        default: false,
    },
    marginLeft: {
        type: Boolean,
        required: false,
        default: false,
    },
    borderTop: {
        type: Boolean,
        required: false,
        default: false,
    },
    borderBottom: {
        type: Boolean,
        required: false,
        default: false,
    },
    radiusTopLeft: {
        type: Boolean,
        required: false,
        default: false,
    },
    radiusTopRight: {
        type: Boolean,
        required: false,
        default: false,
    },
    radiusBottomLeft: {
        type: Boolean,
        required: false,
        default: false,
    },
    radiusBottomRight: {
        type: Boolean,
        required: false,
        default: false,
    },
    top: {
        type: Boolean,
        required: false,
        default: false,
    },
    right: {
        type: Boolean,
        required: false,
        default: false,
    },
    bottom: {
        type: Boolean,
        required: false,
        default: false,
    },
    left: {
        type: Boolean,
        required: false,
        default: false,
    },
    mid: {
        type: Boolean,
        required: false,
        default: false,
    },
  },
}
</script>
<style lang="scss">
  .keeb__case {
    background-color: var(--case-color);
    z-index: 90000;
  }

  //Margin
  .keeb__case--mt {
    margin-top: 1px;
  }
  .keeb__case--mr {
    margin-right: 1px;
  }
  .keeb__case--ml {
    margin-left: 1px;
  }
  .keeb__case--mb {
    margin-bottom: 1px;
  }

  //Border
  .keeb__case--bt {
    border-top: 1px solid var(--case-color); 
  }
  .keeb__case--bb {
    border-bottom: 1px solid var(--case-color); 
  }

  //Radius
  .keeb__case--rtl {
    border-top-left-radius: 6px;
  }
  .keeb__case--rtr {
    border-top-right-radius: 6px;
  }
  .keeb__case--rbl {
    border-bottom-left-radius: 6px;
  }
  .keeb__case--rbr {
    border-bottom-right-radius: 5px;
  }
  // .keeb__case--bt-rad {
  //   border-top-left-radius: 6px;
  //   border-top-right-radius: 6px;
  // }
  // .keeb__case--bb-rad {
  //   border-bottom-left-radius: 6px;
  //   border-bottom-right-radius: 6px;
  // }

  .keeb__case--top {
    height: 15px;
  }
  .keeb__case--mid {
    min-height: 15px;
  }
  .keeb__case--bottom {
    height: 15px;
  }

  .keeb__case.keeb__case--span2 {
    grid-column: span 2;
  }
  .keeb__case.keeb__case--span4 {
    grid-column: span 4;
  }
  .keeb__case.keeb__case--span5 {
    grid-column: span 5;
  }
  .keeb__case.keeb__case--span8 {
    grid-column: span 8;
  }
  .keeb__case.keeb__case--span12 {
    grid-column: span 12;
  }
  .keeb__case.keeb__case--span16 {
    grid-column: span 16;
  }
  .keeb__case.keeb__case--span55 {
    grid-column: span 55;
  }
  .keeb__case.keeb__case--span60 {
    grid-column: span 60;
  }
  .keeb__case.keeb__case--span75 {
    grid-column: span 75;
    height:15px;
  }
</style>
