<template>
  <v-container>
    <v-row class="mt-5">
      <v-spacer></v-spacer>
          <v-col cols="12">
            <v-card>
              <v-card-text>
                <v-form
                  ref="form"
                  v-model="valid"
                  lazy-validation
                  counter
                >
                  <v-file-input
                    v-model="filePeople"
                    accept="text/xml"
                    label="Choose people XML"
                  />
                  <v-file-input
                    v-model="fileShiporder"
                    accept="text/xml"
                    label="Choose shiporder XML"
                  />
                  <v-btn color="success" class="mr-1">
                    Upload files
                  </v-btn>
                  <v-btn color="default">
                    Cancel
                  </v-btn>
                </v-form>
              </v-card-text>
            </v-card>
          </v-col>
      <v-spacer></v-spacer>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "FormUpload",

  data: () => ({
    valid: true,
    filePeople: '',
    fileShiporder: ''
  }),
  methods: {
    validate () {
      this.$refs.form.validate()
    },
    reset () {
      this.$refs.form.reset()
    },
    resetValidation () {
      this.$refs.form.resetValidation()
    },
  }
};
</script>
