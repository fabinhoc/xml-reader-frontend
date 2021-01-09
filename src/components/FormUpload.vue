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
                  <v-btn color="success" class="mr-1" @click="sendFile">
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
      <v-snackbar
        v-model="snackbar"
        :color="color"
      >
        {{ text }}

        <template v-slot:action="{ attrs }">
          <v-btn
            text
            v-bind="attrs"
            @click="snackbar = false"
          >
            Close
          </v-btn>
        </template>
      </v-snackbar>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "FormUpload",

  data () {
    return {
      snackbar: false,
      text: '',
      color:'',
      valid: true,
      filePeople: [],
      fileShiporder: []
    }
  },
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
    async sendFile () {
      const responseShiporder = await this.sendShiporder();
      const responsePeople = await this.sendPeople();
      
      this.snackbar = true
      if (responseShiporder !== 'success' || responsePeople !== 'success') {
        this.color = 'red'
        this.text = responseShiporder + ' ' + responsePeople
      } else {
        this.color = 'success'
        this.text = 'Files has been uplodaded!';
      }

    }, 
    async sendShiporder () {
      let response = 'success'

      if (this.fileShiporder.length !== 0) {

        let formData = new FormData();
        formData.append('file', this.fileShiporder);

        let res = await fetch('http://localhost:8002/api/upload/shiporders', {
          method: 'POST',
          body: formData,
        });

        response = await res.json();
      }

      return response;     
    },
    async sendPeople () {

      let response = 'success'

      if (this.filePeople.length !== 0) {
        let formData = new FormData();
        formData.append('file', this.filePeople);

        let res = await fetch(`http://localhost:8002/api/upload/people`, {
          method: 'POST',
          body: formData,
        });
        
        response = await res.json();
      }

      return response;
    }
  }
};
</script>
