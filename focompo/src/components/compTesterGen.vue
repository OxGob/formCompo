<template>
    <q-card class="bg-cyan-2 q-ma-xl">
        <q-card-main>
             <q-field class="q-mb-sm" label="Form Title Prop: " helper="Please enter the title of the form. This IS displayed to the user.">
                <q-input v-model="fo.mTitle" type="text" align="center" clearable />
            </q-field>
            <q-field class="q-mb-sm" label="Form Description: " helper="Please enter a description for the form. This IS displayed to the user.">
                <q-input v-model="fo.mDescr" type="textarea" rows="5" align="center" clearable />
              </q-field>
            <q-btn class="float-right" label="Save Form / Fire Obj" color="purple" @click="emitToParentObj"/>
        </q-card-main>
    </q-card>
</template>

<script>
export default {
  props: ['formTitle'],
  data () {
    return {
      mutableTitle: '',
      mutDescr: '',
      fo: {
        mTitle: '',
        mDescr: ''
      }
    }
  },
  methods: {
    emitToParent () {
      this.$q.notify('emit to Parent Fired 1:' + this.mutableTitle)
      this.$emit('chiFoTitle', this.mutableTitle)
    },
    emitToParent2 () {
      this.$q.notify('emit to Parent has been Fired 2:' + this.mutDescr)
      this.$emit('chiFoDescr', this.mutDescr)
    },
    emitToParentObj () {
      this.$q.notify('emit to Parent as object Fired 2:' + this.fo)
      console.log('Emit fo  Obj is : ', this.fo)
      this.$emit('chiObjFo', this.fo)
    }
  }
}
</script>
