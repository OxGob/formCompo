<template>
    <q-card class="bg-cyan-2 q-ma-xl">
        <q-card-main>
            <q-field class="q-mb-sm" label="Form Title Prop: " helper="Please enter the title of the form. This IS displayed to the user.">
                <q-input v-model="mutableTitle" type="text" align="center" clearable />
            </q-field>
            <q-btn label="Fire emit" @click="emitToParent"/>
        </q-card-main>
    </q-card>
</template>

<script>
export default {
  props: ['formTitle'],
  data () {
    return {
      mutableTitle: ''
    }
  },
  methods: {
    emitToParent () {
      this.$q.notify('emit to Parent Fired:' + this.mutableTitle)
      this.$emit('chiFoTitle', this.mutableTitle)
    }
  }
}
</script>
