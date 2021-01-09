<template>
  <v-row>
      <v-col cols="12" class="mt-10 text-center">
        <h2 class="font-weight-light">{{ data.name }}</h2>
        <br>
      </v-col>
      <v-col cols="12">
          <h4 class="text-caption">
            <v-icon size="16" class="mt-n1">mdi-phone</v-icon>
            PHONES
          </h4>
          <v-divider />
      </v-col>
      <v-col cols="12" class="mt-n5">
        <v-list-item-group color="primary">
          <v-list-item v-for="item in data.phones" :key="item.id">
            <v-list-item-content>
              <v-list-item-title>{{ item.phone }}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list-item-group>
      </v-col>
      <v-col cols="12">
          <h4 class="text-caption">
            <v-icon size="16" class="mt-n1">mdi-purse</v-icon>
            SHIP ORDER
          </h4>
          <v-divider />
      </v-col>
      <v-col cols="12">
        <v-row>
          <v-col cols="12">
            <v-card>
              <v-card-text>
                <v-row>
                  <v-col cols="12" v-for="item in data.shiporders" :key="item.id">
                    <v-row>
                      <v-col cols="6">
                        <span><b>Id:</b> {{ item.id }}</span>
                        <br>
                        <span><b>Address:</b> {{ item.shipto_address }}</span>  
                        <br>
                        <span><b>Country:</b> {{ item.shipto_country }}</span>  
                      </v-col>
                      <v-col cols="6">
                        <span><b>Name:</b> {{ item.shipto_name }}</span>  
                        <br>
                        <span><b>City:</b> {{ item.shipto_city }}</span>  
                      </v-col>
                    </v-row>
                    <br>
                    <v-row>
                      <v-col cols="12" class="mb-n3">
                        <h6 class="text-caption">
                          <v-icon size="16" class="mt-n1">mdi-plus</v-icon>
                          ITEMS
                        </h6>
                        <v-divider />
                      </v-col>
                      <v-col cols="12">
                        <v-simple-table>
                          <template v-slot:default>
                            <thead>
                              <tr>
                                <th class="text-left">
                                  Id
                                </th>
                                <th class="text-left">
                                  Title
                                </th>
                                <th class="text-left">
                                  Note
                                </th>
                                <th class="text-left">
                                  Quantity
                                </th>
                                <th class="text-left">
                                  Price
                                </th>
                              </tr>
                            </thead>
                            <tbody>
                              <tr
                                v-for="i in item.items"
                                :key="i.name"
                              >
                                <td>{{ i.id }}</td>
                                <td>{{ i.title }}</td>
                                <td>{{ i.note }}</td>
                                <td>{{ i.quantity }}</td>
                                <td>{{ i.price }}</td>
                              </tr>
                            </tbody>
                          </template>
                        </v-simple-table>
                      </v-col>
                    </v-row>
                  </v-col>
                </v-row>
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-col>
  </v-row>
</template>

<script>
export default {
  name: "Detail",
  props: {
    data: Object,
    default: Object
  },
  data () {
    return {
    }
  },
  methods: {
   
  }
};
</script>
