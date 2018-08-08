<template>
    <q-card class="bg-white q-ma-xl">
        <q-card-main>
        <!-- QDes - Forms  -->
             <q-field class="q-mb-sm" label="Form Title Prop: " helper="Please enter the title of the form. This IS displayed to the user.">
                <q-input v-model="formG.fname" type="text" align="center" clearable />
            </q-field>
            <q-field class="q-mb-sm" label="Form Description: " helper="Please enter a description for the form. This IS displayed to the user.">
                <q-input v-model="formG.fDescription" type="textarea" rows="5" align="center" clearable />
            </q-field>
            <q-card-separator class="q-mb-md q-mt-lg"/>
        <!-- QDes - Questions -->
        <!-- QDes - Answers -->
            <q-btn class="q-ml-lg" label="Save Form / Fire Obj" color="purple" @click="emitToParentObj"/>
        </q-card-main>
    </q-card>
</template>

<script>
export default {
  props: ['formTitle'],
  data () {
    return {
      formG:
        {
          // ansRadioVal: '',
          // answers: [
          //   {
          //     questionId: '',
          //     answerText: '',
          //     answerId: '',
          //     timeStamp: ''
          //   }
          // ],
          counterGenQuID: 0,
          // counterAnswers: 0,
          fDescription: '',
          fname: '',
          questions: [
            {
              qtext: '',
              qHelp: '',
              qId: 'Initial Question',
              nextDefaultId: '',
              qType: 'single',
              answerChoices: [
                {
                  answerId: 'Answer 1',
                  text: '',
                  nextQuId: '',
                  showAnswerLabelError: false
                }
              ],
              // ansTrackingID: [
              //   {
              //     ansID: 'Answer 1',
              //     ansIndex: 0
              //   }
              // ],
              counterAnsChID: 0,
              showNextQIdError: false,
              showQIdError: false
            }
          ],
          qTrackingID: [
            {
              quesID: 'Initial Question',
              quesIndex: 0
            }
          ],
          quSelOptions: [
            {
              label: 'Freetext',
              value: 'freetext'
            },
            {
              label: 'Single choice',
              value: 'single'
            }
          ],
          // tempAnsHolder: '',
          trackQuID: ''
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
      console.log('Emit fo  Obj is : ', this.formG)
      this.$emit('chiObjFo', this.formG)
    }
  }
}
</script>
