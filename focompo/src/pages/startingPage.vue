<template>
  <q-page>
    <q-card class="bg-grey-5 q-ma-xl">
      <q-card-main>
        <q-btn label="Add Form" color = "amber" @click="addFormTapped"/>
        <compTestG1 @chiFoTitle="forms.fname = $event"
         @chiFoDescr="forms.fDescription = $event"
         @chiObjFo="tesSeveral = $event"></compTestG1>
        <!-- <compTestG1 :forms.fname /> -->
      </q-card-main>
    </q-card>
  </q-page>
</template>

<script>
import formBuilder from 'components/formBuilder.vue'
import compTestG from 'components/compTesterGen.vue'
export default {
  components: {
    'formBuilder1': formBuilder,
    'compTestG1': compTestG
  },
  data () {
    return {
      someT: '',
      forms:
        {
          fDescription: '',
          fname: ''
        },
      tesSeveral: [{
      }]
    }
  },
  methods: {
    addFormTapped () {
      this.$q.notify('Form added')
    }
  }
}
</script>
