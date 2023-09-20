<template>
 <div>
   <v-data-table
    :headers="headers"
    :items="employeeItem"
    class="elevation-1"
  >
    <template v-slot:top>
      <v-toolbar
        flat
      >
        <v-toolbar-title>จัดการข้อมูล</v-toolbar-title>
        <v-divider
          class="mx-4"
          inset
          vertical
        ></v-divider>
        <v-spacer></v-spacer>
         <v-btn
              color="primary"
              dark
              class="mb-2"
             @click="openDialog('add' , defaultItem)"
            >
              เพิ่มข้อมูล
            </v-btn>
      
      </v-toolbar>
    </template>
    <template v-slot:[`item.role`] ="{ item }">
      {{item.role.name}}
    </template>
    <template v-slot:[`item.actions`]="{ item }">
      <v-icon
        small
        class="mr-2"
        @click="openDialog('edit' , item)"
      >
        mdi-pencil
      </v-icon>
      <v-icon
        small
        @click="deleteItem(item)"
      >
        mdi-delete
      </v-icon>
    </template>
    <template v-slot:no-data>
      <v-btn
        color="primary"
        @click="initialize"
      >
        Reset
      </v-btn>
    </template>
  </v-data-table>
    <v-dialog
          v-model="dialog"
          max-width="500px"
        >
          <v-card>
            <v-card-title>
              <span class="text-h5">{{ formTitle }}</span>
            </v-card-title>

            <v-card-text>
              <v-container>
                <v-row>
                  <v-col
                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                      v-model="firstName"
                      label="ชื่อ"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                      v-model="lastName"
                      label="นามสกุล"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                      v-model="salary"
                      label="เงินเดือน"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                      v-model="role"
                      label="ตำแหน่ง"
                    ></v-text-field>
                  </v-col>
                </v-row>
              </v-container>
            </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                color="blue darken-1"
                text
                @click="close"
              >
                Cancel
              </v-btn>
              <v-btn
                color="blue darken-1"
                text
                @click="save(formTitle)"
              >
                บันทึกข้อมูล
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <v-dialog v-model="dialogDelete" max-width="500px">
          <v-card>
            <v-card-title class="text-h5">คุณต้องการลบข้อมูลในตารางใช่ หรือ ไม่?</v-card-title>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="closeDelete()">ยกเลิก</v-btn>
              <v-btn color="blue darken-1" text @click="deleteItemConfirm()">ตกลง</v-btn>
              <v-spacer></v-spacer>
            </v-card-actions>
          </v-card>
        </v-dialog>
 </div>
</template>

<script>
export default {
    data: () => ({
      firstName: '',
      lastName: '',
      salary: 0,
      role: '',
      idEmployee: 0,
      dialog: false,
      dialogDelete: false,
      headers: [
        {
          text: 'ไอดี',
          align: 'start',
          sortable: false,
          value: 'id',
        },
        { text: 'ชื่อ', value: 'firstName' },
        { text: 'นามสกุล', value: 'lastName' },
        { text: 'เงินเดือน', value: 'salary' },
        { text: 'ตำแหน่ง', value: 'role' },
        { text: 'Actions', value: 'actions', sortable: false },
      ],
      employeeItem: [],
      editedIndex: -1,
      editedItem: {
        name: '',
        calories: 0,
        fat: 0,
        carbs: 0,
        protein: 0,
      },
      defaultItem: {
        name: '',
        calories: 0,
        fat: 0,
        carbs: 0,
        protein: 0,
      },
      formTitle: ''
    }),

    watch: {
      dialog (val) {
        val || this.close()
      },
      dialogDelete (val) {
        val || this.closeDelete()
      },
    },

    created () {
      this.initialize()
    },

    methods: {
     async initialize () {
      this.employeeItem = []  // clear data in font
      try {
        var data = await this.axios.get('http://localhost:9000/employee')
        console.log('data employee  ===> ' ,data)
        this.employeeItem = data.data
      } catch(error) {

      }
      },

      openDialog(Actions ,item){
        //console.log(Actions ,Item)
        this.formTitle = ''
        if(Actions === 'add'){
            this.dialog = true
            this.formTitle = 'เพิ่มข้อมูล'
            this.editedItem = item
        } else {
          console.log(item)
            this.formTitle = 'แก้ไขข้อมูล'
          //  this.editedIndex = this.desserts.indexOf(item)
          //  this.editedItem = item
            this.dialog = true

            this.firstName = item.firstName
            this.lastName = item.lastName
            this.salary = item.salary
            this.role = item.role.name
            this.idEmployee = item.id
        }
        
      },

      editItem (item) {
        this.editedIndex = this.desserts.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialog = true
      },

    deleteItem (item) {
        // this.editedIndex = this.desserts.indexOf(item)
        // this.editedItem = item
         
        this.idEmployee = item.id
        this.dialogDelete = true

       
      },

   async deleteItemConfirm () {
         try {
            var dataResponse = await this.axios.delete('http://localhost:9000/employee/' + this.idEmployee)
            this.initialize()
            console.log('data response ==> ', dataResponse)
          } catch (error) {
            console.log(error.message)
          }
        this.closeDelete()
      },

      close () {
        this.dialog = false
        this.firstName = ''
        this.lastName = ''
        this.salary = ''
        this.role = ''
      },

      closeDelete () {
        this.dialogDelete = false
          this.editedItem = []
          this.editedIndex = -1
      },

      async save (actions) {
        if(actions === 'เพิ่มข้อมูล'){
           // this.desserts.push(this.editedItem) // add data in array dessert 
           // this.close()
          var data = {
            firstName: this.firstName,
            lastName: this.lastName,
            salary: this.salary,
            role: {
              name: this.role
              },
              skills: [
                {skill: ''}
              ]
          }

          console.log('data after send', data)
          try {
            var dataResponse = await this.axios.post('http://localhost:9000/employee' , data)
            this.initialize()
            console.log('data response ==> ', dataResponse)
          } catch (error) {
            console.log(error.message)
          }

        } else {
          //  Object.assign(this.desserts[this.editedIndex] , this.editedItem)
           var data = {
            firstName: this.firstName,
            lastName: this.lastName,
            salary: this.salary,
            role: {
              name: this.role
              },
              skills: [
                {skill: ''}
              ]
          }

          console.log('data after send', data)
          try {
            var dataResponse = await this.axios.put('http://localhost:9000/employee/' + this.idEmployee , data)
            this.initialize()
            console.log('data response ==> ', dataResponse)
          } catch (error) {
            console.log(error.message)
          }
        }
        this.close()
      },
    },

}
</script>

<style>

</style>