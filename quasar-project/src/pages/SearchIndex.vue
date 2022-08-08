<template>
  <q-page class="flex flex-center">
        <div class="q-pa-md">
            <div class="q-gutter-md" style="max-width: 300px">
                <q-input bottom-slots bind:v-model="searchText" label="Label" counter maxlength="12">
                    
                    <template v-slot:after>
                    <q-btn round dense flat icon="send" @click="fetchSearchIndex" />
                    </template>
                </q-input>
                
            </div>
        </div>
  </q-page>
</template>

<script>
import axios from 'axios'
import {ref} from 'vue'

export default {
  setup() {
    const searchText=ref('xyz');
    

    function fetchSearchIndex () {
        console.log(searchText)
        axios.get('http://localhost:8080/search/name/'+searchText.value).then(response => {
            
            alert(response.data.message);
        }).catch(e => {
            console.log(e)
        })
    }

    return {
        fetchSearchIndex
    }
   
  }
}
</script>
