<template lang="pug">
  v-card
    v-toolbar(@click="show = !show")
      v-btn(icon )
        v-icon {{ show ? 'keyboard_arrow_down' : 'keyboard_arrow_up' }}
      v-toolbar-title 能力値
    v-slide-y-transition
      v-container(fluid grid-list-lg v-show="show")
        v-layout(row wrap justify-space-between)
          v-flex(xs4 sm4 md4)
            v-text-field(label="技" v-model.number="baseStatus.gi")
          v-flex(xs4 sm4 md4)
            v-text-field(label="体" v-model.number="baseStatus.tai")
          v-flex(xs4 sm4 md4)
            v-text-field(label="心" v-model.number="baseStatus.shin")
          //-
          v-flex(xs2 sm2 md2)
            v-text-field(label="A" v-model.number="baseStatus.a")
          v-flex(xs2 sm2 md2)
            v-text-field(label="B" v-model.number="baseStatus.b")
          v-flex(xs2 sm2 md2)
            v-text-field(label="C" v-model.number="baseStatus.c")
          v-flex(xs2 sm2 md2)
            v-text-field(label="D" v-model.number="baseStatus.d")
          v-flex(xs2 sm2 md2)
            v-text-field(label="E" v-model.number="baseStatus.e")
          v-flex(xs2 sm2 md2)
            v-text-field(label="F" v-model.number="baseStatus.f")
          //-
          v-flex(xs2 sm2 md2)
            v-text-field(label="成長A" v-model.number="baseStatus.aMod")
          v-flex(xs2 sm2 md2)
            v-text-field(label="成長B" v-model.number="baseStatus.bMod")
          v-flex(xs2 sm2 md2)
            v-text-field(label="成長C" v-model.number="baseStatus.cMod")
          v-flex(xs2 sm2 md2)
            v-text-field(label="成長D" v-model.number="baseStatus.dMod")
          v-flex(xs2 sm2 md2)
            v-text-field(label="成長E" v-model.number="baseStatus.eMod")
          v-flex(xs2 sm2 md2)
            v-text-field(label="成長F" v-model.number="baseStatus.fMod")
          //-
          v-flex(xs2 sm2 md2 v-for="item in endStatus")
            status-card(:list="[{label:item.label,value:item.value},{label:'ボーナス',value:item.bonus}]")
          v-flex(xs2 sm2 md2 v-for="item in calculatedStatus")
            status-card(:list="[{label:item.label,value:item.value}]")
        //- v-divider(v-if="true")
          p hoge

</template>

<script>
import StatusCard from '~/components/parts/common/StatusCard.vue'
export default {
    props: ['baseStatus','endStatus', 'calculatedStatus'],
    data() {
      return {
        show: false
      }
    },
    components: {
      StatusCard,
    }
  }
</script>

<style>

</style>
