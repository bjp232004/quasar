<template>
  <q-page class="flex flex-center">
    <div class="q-pa-md">
    <div class="q-gutter-md row items-start">
      <q-uploader
        style="max-width: 300px"
        url="http://localhost:8080/upload"
        label="Filtered (for <2k size)"
        multiple
        :filter="checkFileSize"
        @rejected="onRejected"
      />

    </div>
  </div>
  </q-page>
</template>

<script>
import { ref } from 'vue'
import { useQuasar } from 'quasar'

export default {
  setup() {
    const $q = useQuasar()

    function checkFileSize (files) {
      return files.filter(file => file.size < 2048)
    }

    function checkFileType (files) {
      return files.filter(file => file.type === 'image/png')
    }

    function onRejected (rejectedEntries) {
        console.log(rejectedEntries);
      // Notify plugin needs to be installed
      // https://quasar.dev/quasar-plugins/notify#Installation
      $q.notify({
        type: 'negative',
        message: `${rejectedEntries.length} file(s) did not pass validation constraints`
      })
    }

    return {
      checkFileSize,
      checkFileType,
      onRejected
    }
  }
}
</script>
