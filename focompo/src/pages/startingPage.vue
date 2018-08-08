<template>
  <q-page>
    <q-card class="bg-cyan-2 q-ma-xl">
      <q-card-main>
        <div v-for="(formG, formInd) in formsg" :key=formG.id>
          <div class="q-mb-md q-mt-lg">
            <q-btn label="Add Form" color = "amber" @click="addFormTapped(formInd)"/>
            <q-btn class="q-ml-md" v-show="formInd !==0" label="Remove Form" color = "pink" @click="removeForm(formInd)"/>
          </div>
          <q-field class="q-mb-sm" label="Form Label: ">
            <q-input v-model="formG.formLabel" type="text" align="center" clearable />
          </q-field>
          <compTestG1 @chiObjForm="formG.formComponentObj = $event"></compTestG1>
          <compoTestV :testvalFromParent='formG'></compoTestV>
          <q-card-separator class="q-mb-md q-mt-lg"/>
        </div>
        <!-- <compTestG1 @chiFoTitle="forms.fname = $event"
         @chiFoDescr="forms.fDescription = $event"
         @chiObjFo="tesSeveral = $event"></compTestG1> -->
        <!-- <compTestG1 :forms.fname /> -->
      </q-card-main>
    </q-card>
    <q-card>
      <!-- <compoTestV :testvalFromParent='this.testval'></compoTestV> -->
    </q-card>
  </q-page>
</template>

<script>
import formBuilder from 'components/formBuilder.vue'
import compTestG from 'components/compTesterGen.vue'
import comTesV from 'components/compTestView.vue'
export default {
  components: {
    'formBuilder1': formBuilder,
    'compTestG1': compTestG,
    'compoTestV': comTesV
  },
  data () {
    return {
      counterFormsg: 0,
      testval: [{test: 'sometng29'}],
      formsg: [
        {
          formLabel: 'form 0',
          formComponentObj: '',
          indexFo: 0
        }
      ],
      formTracker: [
        {
          formTkID: 'form 0',
          indexOfForm: 0
        }
      ]
    }
  },
  methods: {
    addFormTapped (formInd) {
      this.counterFormsg++
      this.$q.notify('Form added. new counter is: ' + this.counterFormsg)
      this.addFormRow(formInd)
    },
    removeForm (formInd) {
      this.formsg.splice(formInd, 1)
      this.updtFormTrackerRemove(formInd)
    },
    addFormRow (formInd) {
      this.formsg.push({
        formLabel: 'Form ' + this.counterFormsg,
        formComponentObj: '',
        indexFo: this.counterFormsg
      })
      this.updtFormTrackerAdd(formInd)
    },
    updtFormTrackerAdd (formInd) {
      var lastIndexFormObj = this.formsg.length - 1
      this.formTracker.push({
        formTkID: this.formsg[lastIndexFormObj].formLabel,
        indexOfForm: lastIndexFormObj
      })
    },
    updtFormTrackerRemove (formInd) {
      var foTk = this.formTracker
      // remove the selected index from the form tracking Array
      foTk.splice(formInd, 1)
      // In the tracking array, update the form index for those removed AFTER SPLICE index
      var lenTrkAfterSplice = foTk.length
      if (formInd < lenTrkAfterSplice) {
      // If formInd is NOT LAST, then from formInd position till last, subtract 1 from values of indexOfForm
        var i
        for (i = formInd; i < lenTrkAfterSplice; i++) {
          var fn = foTk[i].indexOfForm - 1
          foTk[i].indexOfForm = fn
        }
      }
    }
  }
}
</script>
