<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <v-btn
        href="https://github.com/fabinhoc/xml-reader"
        target="_blank"
        text
      >
        <span class="mr-2">XML Reader</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <FormUpload />
      <TableReader />
    </v-main>
  </v-app>
</template>

<script>
import FormUpload from "./components/FormUpload";
import TableReader from "./components/TableReader";

export default {
  name: "App",

  components: {
    FormUpload,
    TableReader
  },

  data: () => ({
    //
  })
};
</script>
