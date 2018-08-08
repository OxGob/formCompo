<template>
  <q-page>
    <q-card class="bg-cyan-2 q-ma-xl">
      <q-card-main>
        <div v-for="(foG, formInd) in formsg" :key=foG.id>
          <q-field class="q-mb-sm" label="Form ID: ">
            <q-input v-model="foG.formID" type="text" align="center" clearable />
          </q-field>
          <q-btn label="Add Form" color = "amber" @click="addFormTapped"/>
          <q-btn class="q-ml-md" label="Remove Form" color = "pink" @click="removeForm(formInd)"/>
        </div>
        <!-- <compTestG1 @chiFoTitle="forms.fname = $event"
         @chiFoDescr="forms.fDescription = $event"
         @chiObjFo="tesSeveral = $event"></compTestG1> -->
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
      counterFormsg: 0,
      formsg: [
        {
          formID: 0,
          indexFo: 0
        }
      ],
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
      this.counterFormsg++
      this.$q.notify('Form added. new counter is: ' + this.counterFormsg)
      this.addFormRow()
    },
    removeForm (index) {
      this.$q.notify('Remove Form')
      this.formsg.splice(index, 1)
    },
    addFormRow () {
      this.formsg.push({
        formID: this.counterFormsg,
        indexFo: this.counterFormsg
      })
    }
  }
}
</script>
