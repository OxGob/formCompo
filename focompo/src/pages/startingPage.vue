<template>
  <q-page>
    <q-card class="bg-cyan-2 q-ma-xl">
      <q-card-main>
        <q-btn label="Add Form" color = "primary" @click="addFormTapped"/>
        <q-card-separator class="q-mb-sm q-mt-md"/>
        <div v-for="(formG, formInd) in formsGen" :key=formG.id>
          <div v-if="formG.rowExists">
            <div class="q-mb-md q-mt-md" v-show="showRowFirstTime">
                <div class="row">
                  <div class="col-5">
                    <q-btn label="Show/Hide Form Builder" v-show="true" color = "green" @click="toggleFoBu(formInd)"/>
                  </div>
                  <div class="col-3"></div>
                  <div class="col-4">
                    <q-btn class="float-right" label="Remove Form" color = "pink" @click="removeForm(formInd)"/>
                  </div>
                </div>
                <q-field class="q-mb-sm" label="Form Label: ">
                  <q-input v-model="formG.formLabel" type="text" align="center" clearable />
                </q-field>
              <!-- GET flag from emitOpenFormViewer in Form Builder to show formViewer. -->
              <div v-show="formG.showFormBuilder">
                <compTestG1 @chiObjForm="formG.formComponentObj = $event" @emitOpenFormViewer="displayFormViewer(formInd)"></compTestG1>
              </div>
              <!-- Use v-if so that on the creation of component formViewer, init() can be run in formViewer -->
              <!-- On returning to its parent, the formViewer component will be destroyed -->
              <div v-if="formG.showFormViewer">
                <!-- Send to component prop (:valFromParent). Receive from child (@returnToParent)   -->
                <compoTestV :valFromParent='formG' @returnToParent="displayFormBuilder(formInd)"></compoTestV>
              </div>
              <q-card-separator class="q-mb-md q-mt-lg"/>
            </div>
          </div>
        </div>
      </q-card-main>
    </q-card>
    <q-card>
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
      counterformsGen: 0,
      removedAllForms: false,
      showRowFirstTime: false,
      formsGen: [
        {
          formLabel: 'form 0',
          formComponentObj: '',
          indexFo: 0,
          rowExists: true,
          showFormBuilder: false,
          showFormViewer: false,
          toggleHideFoBld: false
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
    // Display Form Sections
    displayFormViewer (index) {
      this.$q.notify('displayFormViewer Called: ')
      this.formsGen[index].showFormBuilder = false
      this.formsGen[index].showFormViewer = true
    },
    displayFormBuilder (index) {
      this.$q.notify('displayFormBuilder Called: ')
      this.formsGen[index].showFormBuilder = true
      this.formsGen[index].showFormViewer = false
      this.toggleHideFoBld = true
    },
    toggleFoBu (formInd) {
      if (this.formsGen[formInd].toggleHideFoBld === false) {
        this.formsGen[formInd].showFormBuilder = false
        this.formsGen[formInd].toggleHideFoBld = true
      } else {
        this.formsGen[formInd].showFormBuilder = true
        this.formsGen[formInd].toggleHideFoBld = false
      }
    },
    // Form Row section
    addFormTapped () {
      var formInd = this.formsGen.length - 1
      if (this.removedAllForms === true) {
        this.addFormRow()
        var formIndRAll = this.formsGen.length - 1
        this.displayFormBuilder(formIndRAll)
      } else {
        if (this.counterformsGen === 0) {
          this.showRowFirstTime = true
          this.displayFormBuilder(formInd)
        } else if (this.counterformsGen > 0) {
          this.addFormRow()
          var formInd1 = this.formsGen.length - 1
          this.displayFormBuilder(formInd1)
        }
      }
      this.removedAllForms = false
      this.counterformsGen++
    },
    removeForm (formInd) {
      if (formInd === 0) {
        this.$q.notify('Removing last form')
        this.formsGen[formInd].rowExists = false
        this.formsGen.splice(formInd, 1)
        this.removedAllForms = true
        this.updtFormTracker(formInd)
      } else {
        this.formsGen[formInd].rowExists = false
        this.formsGen.splice(formInd, 1)
        this.updtFormTrackerRemove(formInd)
      }
    },
    addFormRow () {
      this.formsGen.push({
        formLabel: 'Form ' + this.counterformsGen,
        formComponentObj: '',
        indexFo: this.counterformsGen,
        rowExists: true,
        showFormBuilder: true,
        showFormViewer: false,
        toggleHideFoBld: false
      })
      this.updtFormTrackerAdd()
    },
    updtFormTracker (formInd) {
      // at index 0
      this.formTracker[formInd].formTkID = ''
      this.formTracker[formInd].indexOfForm = formInd
    },
    updtFormTrackerAdd () {
      var lastIndexFormObj = this.formsGen.length - 1
      if (this.removedAllForms === false) {
        this.formTracker.push({
          formTkID: this.formsGen[lastIndexFormObj].formLabel,
          indexOfForm: lastIndexFormObj
        })
      } else {
        this.formTracker[0].formTkID = this.formsGen[lastIndexFormObj].formLabel
        this.formTracker[0].indexOfForm = lastIndexFormObj
      }
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
