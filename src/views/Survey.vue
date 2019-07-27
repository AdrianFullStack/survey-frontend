<template>
    <v-layout row pb-2>
        <v-flex xs8 offset-xs2>
            <v-card :class="{ 'card--flex-toolbar': index === 0, 'mt-3': index > 0 }"
                    v-for="(section, index) in sections"
                    :key="index">
                <v-toolbar card prominent>
                    <v-toolbar-title class="body-2 grey--text" style="width: 50%;">
                        <v-text-field
                                v-model="section.title"
                                required
                        ></v-text-field>
                    </v-toolbar-title>

                    <v-spacer></v-spacer>

                    <v-btn icon>
                        <v-icon>add</v-icon>
                    </v-btn>

                    <!--v-btn icon>
                        <v-icon>apps</v-icon>
                    </v-btn>

                    <v-btn icon>
                        <v-icon>more_vert</v-icon>
                    </v-btn-->
                </v-toolbar>

                <v-divider></v-divider>

                <v-card-text>
                    <v-card class="mt-3"
                            v-for="(question, index) in section.questions"
                            :key="index">
                        <v-card-title primary-title>
                            <v-container py-0>
                                <v-layout row justify-space-between>
                                    <v-flex xs12 md6>
                                        <v-text-field
                                                v-model="question.title"
                                                required
                                        ></v-text-field>
                                    </v-flex>
                                    <v-flex xs12 md4>
                                        <v-select
                                                v-model="question.input_type"
                                                :items="input_types"
                                                item-text="name"
                                                item-value="id"
                                                label="Solo field"
                                                solo
                                        ></v-select>
                                    </v-flex>
                                </v-layout>
                                <v-list>
                                    <v-list-tile>
                                        <v-list-tile-action class="justify-center">
                                            <v-icon v-if="question.input_type === 3">radio_button_unchecked</v-icon>
                                            <v-icon v-else-if="question.input_type === 4">check_box_outline_blank</v-icon>
                                            <v-label v-else-if="question.input_type === 5">1</v-label>
                                        </v-list-tile-action>
                                        <v-list-tile-content>
                                            <v-container px-0 py-0>
                                                <v-text-field class="v-text-field-custom"></v-text-field>
                                            </v-container>
                                        </v-list-tile-content>
                                        <v-list-tile-action class="justify-center">
                                            <v-btn icon>
                                                <v-icon>close</v-icon>
                                            </v-btn>
                                        </v-list-tile-action>
                                    </v-list-tile>
                                    <v-list-tile>
                                        <v-list-tile-content>
                                            <v-list-tile-title class="caption">
                                                <a href="khbh">Agregar una opción</a> ó <a href="">AGREGAR "OTROS"</a>
                                            </v-list-tile-title>
                                        </v-list-tile-content>
                                    </v-list-tile>
                                </v-list>
                            </v-container>
                        </v-card-title>
                        <v-divider light></v-divider>
                        <v-card-actions>
                            <v-spacer></v-spacer>
                            <v-btn icon>
                                <v-icon>filter_none</v-icon>
                            </v-btn>
                            <v-btn icon>
                                <v-icon>delete</v-icon>
                            </v-btn>
                            <v-divider
                                    class="mx-4"
                                    inset
                                    vertical
                            ></v-divider>
                            <v-switch
                                    class="pt-0 mt-0"
                                    v-model="question.required"
                                    label="Obligatoria"
                                    color="primary"
                                    hide-details
                                    style="flex: none"></v-switch>
                        </v-card-actions>
                    </v-card>
                </v-card-text>
            </v-card>
        </v-flex>
        <v-fab-transition>
            <v-btn
                    color="pink"
                    dark
                    fab
                    fixed
                    bottom
                    right
                    v-on:click="addSection()"
            >
                <v-icon>add</v-icon>
            </v-btn>
        </v-fab-transition>
    </v-layout>
</template>

<script>
export default {
  name: 'Survey',
  data: () => ({
    input_types: [
      { id: 1, name: 'Respuesta breve' },
      { id: 2, name: 'Parrafo' },
      { id: 3, name: 'Radio buttons' },
      { id: 4, name: 'Casillas de verificación' },
      { id: 5, name: 'Lista desplegable' },
      { id: 6, name: 'Carga de archivos' },
      { id: 7, name: 'Fecha' },
      { id: 8, name: 'Hora' }
    ],
    sections: [
      {
        title: 'Seccion 1',
        questions: [
          {
            title: '¿Cúantos años tienes?',
            input_type: 1,
            required: false,
            options: []
          },
          {
            title: '¿Cúantos años tienes?',
            input_type: 1,
            required: false,
            options: []
          }
        ]
      }
    ]
  }),
  methods: {
    addSection () {
      this.sections.push({ title: `Seccion ${this.sections.length + 1}`, questions: [] })
    }
  }
}
</script>

<style scoped>
    .card--flex-toolbar {
        margin-top: -64px;
    }

    .v-text-field-custom {
        padding-top: 0;
    }

    .v-input__slot {
        margin-top: 5px !important;
    }
</style>
