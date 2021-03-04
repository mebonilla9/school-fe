<template>
  <q-layout
    style="background: linear-gradient(90deg, rgba(58,69,180,0.692612079011292) 0%, rgba(29,143,253,0.8018557764902836) 50%, rgba(69,252,231,0.6589986336331408) 100%)"
  >
    <div class="row justify-around">
      <div class="content">
        <q-card bordered class="q-pa-md shadow-1 form">
          <q-card-section>
            <q-form
              class="row q-col-gutter-x-md  justify-center "
              @submit.prevent="sendRegister"
            >
              <div>
                <h4 class="tittle">Formulario</h4>
              </div>

              <q-input
                class="input"
                bg-color="grey-2"
                square
                filled
                clearable
                v-model="user.document"
                type="text"
                label="Documento"
                lazy-rules
                :rules="[
                  val =>
                    (val && val.length > 0) || 'Por favor escriba su codigo'
                ]"
              />
              <q-input
                class="input"
                bg-color="grey-2"
                filled
                clearable
                v-model="user.name"
                type="text"
                label="Nombre"
                lazy-rules
                :rules="[
                  val =>
                    (val && val.length > 3) || 'Por favor escriba su nombre'
                ]"
              />
              <q-input
                class="input"
                bg-color="grey-2"
                square
                filled
                clearable
                v-model="user.age"
                type="number"
                label="Edad"
                lazy-rules
                :rules="[
                  val =>
                    (val && val.length > 0) ||
                    'Por favor escriba una edad correcta'
                ]"
              />
              <q-card-actions class="q-px-md justify-center">
                <q-btn
                  unelevated
                  color="light-blue-12"
                  size="lg"
                  type="submit"
                  class="field-width"
                  label="Registrar"
                />
              </q-card-actions>
            </q-form>
          </q-card-section>
        </q-card>
      </div>
      <q-card bordered class="q-pa-md shadow-1 stable">
        <div class="table">
          <div>
            <h4 class="tittletable">Registro</h4>
          </div>
          <q-table :data="data" :columns="columns" row-key="id" />
        </div>
      </q-card>
    </div>
  </q-layout>
</template>
<script>
import Axios from 'axios'
export default {
  name: 'Login',
  data () {
    return {
      user: {
        id: '',
        name: '',
        age: 0,
        document: ''
      },
      id: '',
      columns: [
        {
          name: 'document',
          align: 'left',
          label: 'Documento',
          field: 'document'
        },
        {
          name: 'name',
          align: 'left',
          label: 'Nombre',
          field: 'name'
        },

        {
          name: 'age',
          label: 'Edad',
          field: 'age',
          sortable: true,
          align: 'left'
        }
      ],
      data: []
    }
  },
  methods: {
    sendRegister () {
      Axios.post('/student', {
        ...this.user
      })
        .then(resp => {
          this.getData()
        })
        .catch(err => {
          console.log(err)
        })
    },
    getData () {
      Axios.get('/student')
        .then(resp => {
          this.data = resp.data
        })
        .catch(err => {
          console.log(err)
        })
    }
  },
  mounted () {
    this.getData()
  }
}
</script>
