<template>
  <q-page>
    <q-card class="bg-cyan-2 q-ma-xl">
      <q-card-main>
        <!-- <formBuilder1></formBuilder1> -->
        <compTest1></compTest1>
      </q-card-main>
    </q-card>
  </q-page>
</template>

<script>
import formBuilder from 'components/formBuilder.vue'
import compTest from 'components/compTester.vue'
export default {
  components: {
    'formBuilder1': formBuilder,
    'compTest1': compTest
  },
  data () {
    return {
      forms: [
        {
          fDescription: '',
          fname: ''
        }
      ]
    }
  }
}
</script>
