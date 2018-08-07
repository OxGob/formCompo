<template>
    <q-card class="bg-cyan-2 q-ma-xl">
        <q-card-main>
            <q-field class="q-mb-sm" label="Form Title Prop: " helper="Please enter the title of the form. This IS displayed to the user.">
                <q-input v-model="formTitle" type="text" align="center" clearable />
            </q-field>
        </q-card-main>
    </q-card>
</template>

<script>
export default {
  props: ['formTitle'],
  data () {
    return {

    }
  }
}
</script>
