<template>
  <div class="q-pa-md" style="max-width: 400px">

    <q-form
      @submit="onSubmit"
      @reset="onReset"
      class="q-gutter-md"
    >
    <q-input
        filled
        v-model="language"
        label="ภาษา *"
        hint="ภาษา"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'เปลี่ยนภาษา']"
      />
    <!-- ID -->
    <q-input
        filled
        v-model="id"
        label="Your are id *"
        hint="ID"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'Please Enter ID code']"
      />

    <!--name -->
      <q-input
        filled
        v-model="name"
        label="Your name *"
        hint="Name"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'Please type your name']"
      />
    <!-- surname -->
      <q-input
        filled
        v-model="surname"
        label="Your surname *"
        hint="Surname"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'Please type your Surname']"
      />

      <q-input
        filled
        type="number"
        v-model="age"
        label="Your age *"
        lazy-rules
        :rules="[
          val => val !== null && val !== '' || 'Please type your age',
          val => val > 0 && val < 100 || 'Please type a real age'
        ]"
      />

      <q-toggle v-model="accept" label="I accept the license and terms" />

      <div>
        <q-btn label="Submit" type="submit" color="primary"/>
        <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
      </div>
    </q-form>

  </div>
</template>

<script>
import { useQuasar } from 'quasar'
import { ref } from 'vue'

export default {
  setup () {
    const $q = useQuasar()
    const language = ("ภาษาไทย")
    const id =ref("6604101340")
    const name = ref("ธีรศักดิ์")
    const surname=ref("แก้วภา")
    const age = ref(null)
    const accept = ref(false)

    return {
      language,
      id,
      name,
      surname,
      age,
      accept,

      onSubmit () {
        if (accept.value !== true) {
          $q.notify({
            color: 'red-5',
            textColor: 'white',
            icon: 'warning',
            message: 'You need to accept the license and terms first'
          })
        }
        else {
          $q.notify({
            color: 'green-4',
            textColor: 'white',
            icon: 'cloud_done',
            message: 'Submitted'
          })
        }
      },

      onReset () {
        id.value =null
        name.value = null
        surname.value = null
        age.value = null
        language.value = null
        accept.value = false
      }
    }
  }
}
</script>
