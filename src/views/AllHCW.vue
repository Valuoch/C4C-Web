<template>
  <div v-if="user.role_id === 1">
    <v-toolbar-title tabs>
     
      <v-tabs grow
        slot="extension"
        v-model="tabs"
        fixed-tabs
        color="transparent"
        >
        <v-tabs-slider></v-tabs-slider>

        <v-tab href="#mobile-tabs-5-1" class="primary--text">
          <v-icon>Health Care response Complete Profiles</v-icon>
        </v-tab>

        <v-tab href="#mobile-tabs-5-2" class="primary--text">
          <v-icon>Health Care Workers Incomplete Profiles</v-icon>
        </v-tab>
      
      </v-tabs>

    </v-toolbar-title>

    <v-tabs-items v-model="tabs" class="white elevation-1">

      <v-tab-item
        v-for="i in 2"
        :key="i"
        :id="'mobile-tabs-5-' + i"
        >
        <v-container v-if="i===1"
          fill-height
          fluid
          grid-list-xl
          >

          <v-layout 
            justify-center
            wrap
          >
            <v-flex
              md12
              >
              <v-snackbar
                color="error"
                v-model="snackbar"
                :timeout="12000"
                top>
                <v-icon
                  color="white"
                  class="mr-3"
                  >
                  mdi-bell-plus
                </v-icon>
                <div> {{result}}</div>
                <v-icon
                  size="16"
                  @click="snackbar = false"
                >
                  mdi-close-circle
                </v-icon>
              </v-snackbar>
              <v-card>
                <v-card-title>
                  
                   <v-flex
                    xs12
                    md6>
                  <v-text-field
                    v-model="search"
                    append-icon="mdi-magnify"
                    label="Search"
                    single-line
                    hide-details
                  />
                   </v-flex>
                   
                  <v-flex
                    xs12
                    md6>
                    <v-btn
                      :loading="downloadLoading"
                      color="primary"
                      @click="handleDownload">
                      <v-icon left>mdi-download</v-icon>Export Excel
                    </v-btn>
                  </v-flex>
                </v-card-title>

                <v-data-table
                  :headers="headers"
                  :items="all_hcws"
                  :rows-per-page-items="rowsPerPageItems"
                  :search="search"
                  :loading="true"
                  class="elevation-1"
                  item-key="id"
                >

                <template slot='no-data'>
                    <v-progress-linear slot='progress' indeterminate></v-progress-linear>
                </template>

                  <template
                    slot="items"
                    slot-scope="props">
                      <!-- <td>{{ props.item.first_name }}</td>
                      <td>{{ props.item.surname }}</td> -->
                      <td>{{ props.item.gender }}</td>
                      <td>{{ props.item.dob }}</td>
                      <td>{{ props.item.facility_name }}</td>
                      <td>{{ props.item.county }}</td>
                      <td>{{ props.item.sub_county }}</td>
                      <td>{{ props.item.department }}</td>
                      <td>{{ props.item.cadre }}</td>
                  </template>
                  <v-alert
                    slot="no-results"
                    :value="true"
                    color="success"
                    icon="mdi-emoticon-sad">
                    Your search for "{{ search }}" found no results.
                  </v-alert>

                </v-data-table>
              </v-card>
            </v-flex>

          </v-layout>

        </v-container>


         <v-container v-if="i===2"
          fill-height
          fluid
          grid-list-xl
          >

          <v-layout 
            justify-center
            wrap
          >
            <v-flex
              md12
              >
              <v-snackbar
                color="error"
                v-model="snackbar"
                :timeout="12000"
                top>
                <v-icon
                  color="white"
                  class="mr-3"
                  >
                  mdi-bell-plus
                </v-icon>
                <div> {{result}}</div>
                <v-icon
                  size="16"
                  @click="snackbar = false"
                >
                  mdi-close-circle
                </v-icon>
              </v-snackbar>
              <v-card>
                <v-card-title>
                   <v-flex
                    xs12
                    md6>
                  <v-text-field
                    v-model="search"
                    append-icon="mdi-magnify"
                    label="Search"
                    single-line
                    hide-details
                  />
                   </v-flex>
                   
                  <v-flex
                    xs12
                    md6>
                    <v-btn
                      :loading="downloadLoading"
                      color="primary"
                      @click="handleDownload2">
                      <v-icon left>mdi-download</v-icon>Export Excel
                    </v-btn>
                  </v-flex>

                </v-card-title>

  

                <v-data-table
                  :headers="headers1"
                  :items="filteredList"
                  :rows-per-page-items="rowsPerPage"
                  :search="search"
                  :loading="true"
                  class="elevation-1"
                  item-key="id"
                >

                <template slot='no-data'>
                    <v-progress-linear slot='progress' indeterminate></v-progress-linear>
                </template>

                  <template
                    slot="items" slot-scope="props">
                    <!-- v-if="props.item.profile_complete === 0"> -->
                      <!-- <td>{{ props.item.first_name }}</td>
                      <td>{{ props.item.surname }}</td> -->
                      <td>{{ props.item.gender }}</td>
                      <td>{{ props.item.msisdn }}</td>
                      <td>{{ props.item.email }}</td>

                  </template>
                  <v-alert
                    slot="no-results"
                    :value="true"
                    color="success"
                    icon="mdi-emoticon-sad">
                    Your search for "{{ search }}" found no results.
                  </v-alert>

                </v-data-table>
              </v-card>
            </v-flex>

          </v-layout>

        </v-container>

      </v-tab-item>
   </v-tabs-items>
  </div>

  <v-container v-else-if="user.role_id === 2"
    fill-height
    fluid
    grid-list-xl
    >
    <v-layout
      justify-center
      wrap
    >

      <v-flex
        md12
      >

      <v-snackbar
        color="error"
        v-model="snackbar"
        :timeout="12000"
        top>
        <v-icon
        color="white"
        class="mr-3"
      >
        mdi-bell-plus
      </v-icon>
      <div> {{result}}</div>
      <v-icon
        size="16"
        @click="snackbar = false"
      >
        mdi-close-circle
      </v-icon>
      </v-snackbar>

        <v-card>
          <v-card-title>
            All Users
            <v-spacer/>
            <v-text-field
              v-model="search"
              append-icon="mdi-magnify"
              label="Search"
              single-line
              hide-details
            />

            <v-flex
              xs12
              md2>
              <v-btn
                :loading="downloadLoading"
                color="primary"
                @click="handleDownload">
                <v-icon left>mdi-download</v-icon>Export Excel
              </v-btn>
            </v-flex>


          </v-card-title>

          <v-data-table
                  :headers="headers"
                  :items="all_hcws"
                  :rows-per-page-items="rowsPerPageItems"
                  :search="search"
                  :loading="true"
                  class="elevation-1"
                  item-key="id"
                >

                <template slot='no-data'>
                    <v-progress-linear slot='progress' indeterminate></v-progress-linear>
                </template>

                  <template
                    slot="items"
                    slot-scope="props">
                      <!-- <td>{{ props.item.first_name }}</td>
                      <td>{{ props.item.surname }}</td> -->
                      <td>{{ props.item.gender }}</td>
                      <td>{{ props.item.dob }}</td>
                      <td>{{ props.item.facility_name }}</td>
                      <td>{{ props.item.county }}</td>
                      <td>{{ props.item.sub_county }}</td>
                      <td>{{ props.item.department }}</td>
                      <td>{{ props.item.cadre }}</td>

          </template>
            <v-alert
              slot="no-results"
              :value="true"
              color="success"
              icon="mdi-emoticon-sad">
              Your search for "{{ search }}" found no results.
            </v-alert>

          </v-data-table>

        </v-card>

      </v-flex>

    </v-layout>
  </v-container>

   <v-container v-else-if="user.role_id === 5"
    fill-height
    fluid
    grid-list-xl
    >
    <v-layout
      justify-center
      wrap
    >

      <v-flex
        md12
      >

      <v-snackbar
        color="error"
        v-model="snackbar"
        :timeout="12000"
        top>
        <v-icon
        color="white"
        class="mr-3"
      >
        mdi-bell-plus
      </v-icon>
      <div> {{result}}</div>
      <v-icon
        size="16"
        @click="snackbar = false"
      >
        mdi-close-circle
      </v-icon>
      </v-snackbar>

        <v-card>
          <v-card-title>
            All Users
            <v-spacer/>
            <v-text-field
              v-model="search"
              append-icon="mdi-magnify"
              label="Search"
              single-line
              hide-details
            />

            <v-flex
              xs12
              md2>
              <v-btn
                :loading="downloadLoading"
                color="primary"
                @click="handleDownload">
                <v-icon left>mdi-download</v-icon>Export Excel
              </v-btn>
            </v-flex>


          </v-card-title>

          <v-data-table
                  :headers="headers"
                  :items="filteredUsers"
                  :rows-per-page-items="rowsPerPageItems"
                  :search="search"
                  :loading="true"
                  class="elevation-1"
                  item-key="id"
                >

                <template slot='no-data'>
                    <v-progress-linear slot='progress' indeterminate></v-progress-linear>
                </template>

                  <template
                    slot="items"
                    slot-scope="props">

                      <!-- <td>{{ props.item.first_name }}</td>
                      <td>{{ props.item.surname }}</td> -->
                      <td>{{ props.item.gender }}</td>
                      <td>{{ props.item.dob }}</td>
                      <td>{{ props.item.facility_name }}</td>
                      <td>{{ props.item.county }}</td>
                      <td>{{ props.item.sub_county }}</td>
                      <td>{{ props.item.department }}</td>
                      <td>{{ props.item.cadre }}</td>

          </template>
            <v-alert
              slot="no-results"
              :value="true"
              color="success"
              icon="mdi-emoticon-sad">
              Your search for "{{ search }}" found no results.
            </v-alert>

          </v-data-table>

        </v-card>

      </v-flex>

    </v-layout>
  </v-container>

  
  <v-container v-else-if="user.role_id === 4"
    fill-height
    fluid
    grid-list-xl
    >
    <v-layout
      justify-center
      wrap
    >

      <v-flex
        md12
      >

      <v-snackbar
        color="error"
        v-model="snackbar"
        :timeout="12000"
        top>
        <v-icon
        color="white"
        class="mr-3"
      >
        mdi-bell-plus
      </v-icon>
      <div> {{result}}</div>
      <v-icon
        size="16"
        @click="snackbar = false"
      >
        mdi-close-circle
      </v-icon>
      </v-snackbar>

        <v-card>
          <v-card-title>
            All Users
            <v-spacer/>
            <v-text-field
              v-model="search"
              append-icon="mdi-magnify"
              label="Search"
              single-line
              hide-details
            />

            <v-flex
              xs12
              md2>
              <v-btn
                :loading="downloadLoading"
                color="primary"
                @click="handleDownload">
                <v-icon left>mdi-download</v-icon>Export Excel
              </v-btn>
            </v-flex>


          </v-card-title>

          <v-data-table
                  :headers="headers"
                  :items="all_hcws"
                  :rows-per-page-items="rowsPerPageItems"
                  :search="search"
                  :loading="true"
                  class="elevation-1"
                  item-key="id"
                >

                <template slot='no-data'>
                    <v-progress-linear slot='progress' indeterminate></v-progress-linear>
                </template>

                  <template
                    slot="items"
                    slot-scope="props">
                      <!-- <td>{{ props.item.first_name }}</td>
                      <td>{{ props.item.surname }}</td> -->
                      <td>{{ props.item.gender }}</td>
                      <td>{{ props.item.dob }}</td>
                      <td>{{ props.item.facility_name }}</td>
                      <td>{{ props.item.county }}</td>
                      <td>{{ props.item.sub_county }}</td>
                      <td>{{ props.item.department }}</td>
                      <td>{{ props.item.cadre }}</td>

          </template>
            <v-alert
              slot="no-results"
              :value="true"
              color="success"
              icon="mdi-emoticon-sad">
              Your search for "{{ search }}" found no results.
            </v-alert>

          </v-data-table>

        </v-card>

      </v-flex>

    </v-layout>
  </v-container>

</template>


<script>
import axios from 'axios'
import { mapGetters } from 'vuex'
export default {
  data () {
    return {
      n: null,
      new_users: [],
      county_users: [],
      users_ttl: [],
      all_hcws: [],  
      incompletes: [],
      search: '',
      tabs: null,
      isLoading: true,
      snackbar: false,
      result: '',
      rowsPerPageItems: [200, 1000, 5000, 10000],
      rowsPerPage: [1000, 5000, 10000],
      headers: [
        // {
        //   sortable: false,
        //   text: 'First Name',
        //   value: 'first_name'
        // },
        // {
        //   sortable: false,
        //   text: 'Surname',
        //   value: 'surname'
        // },
        {
          sortable: false,
          text: 'Gender',
          value: 'gender'
        },
        {
          sortable: false,
          text: 'Date Of Birth',
          value: 'dob'
        },
        {
          sortable: false,
          text: 'Facility',
          value: 'facility_name'
        },
        {
          sortable: false,
          text: 'County',
          value: 'county'
        },
        {
          sortable: false,
          text: 'Sub County',
          value: 'sub_county'
        },
        {
          sortable: false,
          text: 'Department',
          value: 'department'
        },
        {
          sortable: false,
          text: 'Cadre',
          value: 'cadre'
        },
      ],

      headers1: [
        // {
        //   sortable: false,
        //   text: 'First Name',
        //   value: 'first_name'
        // },
        // {
        //   sortable: false,
        //   text: 'Surname',
        //   value: 'surname'
        // },
        {
          sortable: false,
          text: 'Gender',
          value: 'gender'
        },
        {
          sortable: false,
          text: 'Phone Number',
          value: 'msisdn'
        },
        {
          sortable: false,
          text: 'Email',
          value: 'email'
        }
      ],
      downloadLoading: false,
      filename: `Health care workers ${new Date().toISOString()}`,
      autoWidth: true,
      bookType: 'xlsx'
    }
  },
  computed: {
    ...mapGetters({
      user: 'auth/user',
    }),

    filteredList() {
      let self = this;

      return this.new_users = this.users_ttl.filter(item => item.profile_complete === 0);

    },

    filteredUsers() {
      let self = this;

      return this.county_users = this.all_hcws.filter(item => item.county === this.user.county);

    }

  },
  created () {
    this.getHCW()
    this.getUsers()
  },
  methods: {

    getHCW () {
      if (this.user.role_id === 1 ) {
        axios.get('hcw')
          .then((hcws) => {
            this.all_hcws = hcws.data.data

            this.loopH(hcws.data.links.next)
            this.isLoading = false
          })
          .catch(() => {
            this.result = 'Check your internet connection or retry logging in.'
            this.snackbar = true    
          })
      } else if(this.user.role_id === 2) {
          axios.get(`hcw/partner/${this.user.hcw.partner_id}`)
          .then((hcws) => {
            this.all_hcws = hcws.data.data

            console.log("ndani", this.all_hcws)

            this.loopH(hcws.data.links.next)
            this.isLoading = false

          })
          .catch(() => {
            this.error = true
            this.result = 'Check your internet connection or retry logging in.'
            this.snackbar = true

          })

      } else if(this.user.role_id === 5) {
          axios.get('hcw')
          .then((hcws) => {
            this.all_hcws = hcws.data.data

            this.loopH(hcws.data.links.next)
            this.isLoading = false

          })
          .catch(() => {
            this.error = true
            this.result = 'Check your internet connection or retry logging in.'
            this.snackbar = true

          })

      } else if (this.user.role_id === 4) {
        axios.get(`hcw/facility/${this.user.hcw.facility_id}`)
          .then((hcws) => {
            this.all_hcws = hcws.data.data

            this.loopH(hcws.data.links.next)
            this.isLoading = false
          })
          .catch(() => {
            this.result = 'Check your internet connection or retry logging in.'
            this.snackbar = true
          })
      }
    },
    async loopH (l) {
      var i
      for (i = 0; i < 1;) {
        if (l != null) {
          let response = await axios.get(l)
          l = response.data.links.next
          this.all_hcws = this.all_hcws.concat(response.data.data)
        } else {
          i = 200
        }
      }
    },
    handleDownload () {
      this.downloadLoading = true
      import('@/vendor/Export2Excel').then(excel => {
        const tHeader = ['First Name', 'Surname', 'Gender', 'Mobile', 'Date Of Birth', 'Facility', 'County', 'Sub County', 'Department', 'Cadre', 'Registration Date']
        const filterVal = ['first_name', 'surname','gender', 'msisdn', 'dob', 'facility_name', 'county', 'sub_county', 'department', 'cadre', 'created_at']
        const list = this.all_hcws
        const data = this.formatJson(filterVal, list)
        excel.export_json_to_excel({
          header: tHeader,
          data,
          filename: this.filename,
          autoWidth: this.autoWidth,
          bookType: this.bookType
        })
        this.downloadLoading = false
      })
    },
    formatJson (filterVal, jsonData) {
      return jsonData.map(v => filterVal.map(j => {
        if (v[j] === 'surname') {
          return v[j]
        } else {
          return v[j]
        }
      }))
    },

    getUsers () {
      axios.get('users')
        .then((response) => {

          this.users_ttl = response.data.data

          this.loopT(response.data.links.next)
          this.isLoading = false
        })
        .catch((error) => {
          console.log(error)
          this.error = true
          this.result = 'Check your internet connection or retry logging in.'
          this.snackbar = true

        })
    },

    async loopT (l) {
      var i
      for (i = 0; i < 1;) {
        if (l != null) {
          let response = await axios.get(l)
          l = response.data.links.next
          this.users_ttl = this.users_ttl.concat(response.data.data)
        } else {
          i = 200
        }
      } 
    },

    handleDownload2 () {
      this.downloadLoading = true
      import('@/vendor/Export2Excel').then(excel => {
        const tHeader = ['First Name', 'Surname', 'Gender', 'Phone Number', 'Email', 'Registration Date']
        const filterVal = ['first_name', 'surname', 'gender', 'msisdn', 'email', 'created_at']
        const list = this.new_users
        const data = this.formatJson(filterVal, list)
        excel.export_json_to_excel({
          header: tHeader,
          data,
          filename: this.filename,
          autoWidth: this.autoWidth,
          bookType: this.bookType
        })
        this.downloadLoading = false
      })
    },
    formatJson (filterVal, jsonData) {
      return jsonData.map(v => filterVal.map(j => {
        if (v[j] === 'surname') {
          return v[j]
        } else {
          return v[j]
        }
      }))
    }  

  }
}
</script>
  
