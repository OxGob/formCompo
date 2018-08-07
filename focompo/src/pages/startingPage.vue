<template>
  <q-page>
    <q-card class="bg-cyan-2 q-ma-xl">
      <q-card-main>
        <!-- <formBuilder1></formBuilder1> -->
        <!-- <q-field class="q-mb-sm" label="Form Title: " helper="Please enter the title of the form. This IS displayed to the user.">
            <q-input v-model="forms.fname" type="text" align="center" clearable />
          </q-field> -->
        <compTestG1 @chiFoTitle="forms.fname = $event" @chiFoDescr="forms.fDescription = $event"></compTestG1>
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
      tesSeveral: {
      }
    }
  }
}
</script>
