<template lang="pug">
v-container(grid-list-md text-xs-center)
  h2 {{ $route.params.id }}
  p LV:{{totalMagicalLevel}}
  v-layout(row justify-space-between)
    v-flex(xs9 sm9 md9)
      v-text-field(label="キャラクター名" pa0 ma0)
    v-flex(xs3 sm3 md3)
      v-text-field(label="プレイヤー名" pa0 ma0)
  v-layout(row justify-space-between)
    v-flex(xs6 sm6 md6)
      v-text-field(label="種族" pa0 ma0)
    v-flex(xs3 sm3 md3)
      v-text-field(label="年齢" pa0 ma0)
    v-flex(xs3 sm3 md3)
      v-text-field(label="性別" pa0 ma0)
  status(:baseStatus="cData.status", :endStatus="endStatus", :calculatedStatus="calculatedStatus")
    

</template>

<script>
import Logo from '~/components/Logo.vue'
import VuetifyLogo from '~/components/VuetifyLogo.vue'
import Status from '~/components/parts/sw25/Status.vue'

export default {
  components: {
    Logo,
    VuetifyLogo,
    Status
  },
  data() {
    return {
      cData: {
        status: {
          gi  : 5, 
          tai : 9,
          shin: 15,
          a   : 1,
          b   : 2,
          c   : 3,
          d   : 4,
          e   : 5,
          f   : 6,
          aMod: 1,
          bMod: 2,
          cMod: 3,
          dMod: 4,
          eMod: 5,
          fMod: 6,
        },
        physicalClass: {
          fighter: 1,
          grappler: 0,
          fencer: 2,
          shooter: 0,
        },
        magicalClass: {
          sorcerer: 0,
          conjurer: 1,
          priest: 0,
          magitech: 3,
        },
        otherClass: {
          scout: 0,
          ranger: 1,
          sage: 0,
        }
      }
    }
  },
  computed: {
    endStatus() {
      return {
        dex: this.createStatusInfo("器用度",[this.cData.status.gi   , this.cData.status.a , this.cData.status.aMod]),
        agl: this.createStatusInfo("敏捷度",[this.cData.status.gi   , this.cData.status.b , this.cData.status.bMod]),
        str: this.createStatusInfo("筋力"  ,[this.cData.status.tai  , this.cData.status.c , this.cData.status.cMod]),
        vit: this.createStatusInfo("生命力",[this.cData.status.tai  , this.cData.status.d , this.cData.status.dMod]),
        int: this.createStatusInfo("知力"  ,[this.cData.status.shin , this.cData.status.e , this.cData.status.eMod]),
        mnd: this.createStatusInfo("精神力",[this.cData.status.shin , this.cData.status.f , this.cData.status.fMod]),
      }
    },
    calculatedStatus() {
      return {
        hpMax:     {label: "最大HP",   value: (this.characterLevel * 3 + this.endStatus.vit.value)} ,
        mpMax:     {label: "最大MP",   value: (this.totalMagicalLevel * 3 + this.endStatus.mnd.value)},
        move :     {label: "移動力",   value: (this.endStatus.agl.value)},
        dash :     {label: "全力移動", value: (this.endStatus.agl.value * 3)},
        vitResist: {label: "生命抵抗", value: (this.characterLevel + this.endStatus.vit.bonus)},
        mndResist: {label: "精神抵抗", value: (this.characterLevel + this.endStatus.mnd.bonus)},
      }
    },
    characterLevel() {
      var p = Math.max.apply(null,Object.values(this.cData.physicalClass));
      var m = Math.max.apply(null,Object.values(this.cData.magicalClass));
      var o = Math.max.apply(null,Object.values(this.cData.otherClass));
      return Math.max(p,m,o);
      // return p;
    },
    totalMagicalLevel() {
      var v = 0;
      for(var key in this.cData.magicalClass) {
        v += this.cData.magicalClass[key];
      }
      return v;
    }
  },
  methods: {
    createStatusInfo(lbl,vals) {
      var v = 0;
      vals.forEach(function(val,index,ar){
        v +=  (val==="" || isNaN(val)) ? 0 : parseInt(val);
      });
      return {
        label : lbl,
        value : v,
        bonus : Math.floor(v/6),
      }
    }
  }
}

</script>

