<template>
  <v-container>
    <v-row class="mt-5">
      <v-col cols="12">
        <v-card>
          <v-card-title>
            <v-icon class="mr-1 mt-n1">mdi-account-group</v-icon>
            People list
          </v-card-title>
          <v-card-text>
            <v-row>
              <v-col cols="12">
                <v-btn color="pink darken-1" @click="getData" dark>
                  <v-icon class="mr-1">mdi-refresh</v-icon>
                  <span>
                    Refresh values
                  </span>
                </v-btn>
              </v-col>
              <br>
            </v-row>
            <v-data-table
              :loading="loading"
              :headers="headers"
              :items="data"
              :items-per-page="5"
              class="elevation-1"
            >
              <template v-slot:item.phone="{ item }">
                <v-tooltip bottom color="third">
                  <template v-slot:activator="{ on, attrs }">
                    <a
                      v-bind="attrs"
                      v-on="on"
                      @click="details(item)"
                    >
                      View phones
                    </a>
                  </template>
                  <span class="white--text">See Phone numbers</span>
                </v-tooltip>
              </template>
              <template v-slot:item.shiporder="{ item }">
                <v-tooltip bottom color="third">
                  <template v-slot:activator="{ on, attrs }">
                    <a
                      v-bind="attrs"
                      v-on="on"
                      @click="details(item)"
                    >
                      View Shiporders
                    </a>
                  </template>
                  <span class="white--text">See Shiporders</span>
                </v-tooltip>
              </template>
            </v-data-table>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
    <v-dialog v-model="dialog" width="600">
      <v-card>
        <v-card-text>
          <Detail :data.sync="itemSelected" />
        </v-card-text>
      </v-card>
    </v-dialog>
  </v-container>
</template>

<script>
import Detail from './Detail';

export default {
  name: "TableReader",
  components:{
    Detail
  },
  data () {
    return {
      dialog: false,
      loading: true,
      itemSelected: {},
      data:[],
      headers: [
        {
          text: '#',
          align: 'center',
          sortable: true,
          value: 'id',
        },
        {
          text: 'Name',
          align: 'center',
          sortable: true,
          value: 'name',
        },
        { text: 'Phone', align: 'center', value: 'phone' },
        { text: 'Shiporders', align: 'center', value: 'shiporder' }
      ],
    }
  },
  created () {
    this.getData()
  },
  methods: {
    async getData() {
      this.loading = true
      const res = await fetch('http://localhost:8002/api/people')
      const data = await res.json()
      this.data = data;
      this.loading = false
    },
    details (item) {
      this.dialog = true
      this.itemSelected = item
    }
  }
};
</script>
