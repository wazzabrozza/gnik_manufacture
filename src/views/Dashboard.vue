<template>
<div class="d-flex">
  <sidebar></sidebar>
<v-container class="col-7" fluid>
    <div class="dashboard-page">
      <v-row no-gutters class="d-flex justify-space-between mt-10 mb-6">
        <h1 class="page-title">My Products</h1>
       <v-dialog
      v-model="productsDialog"
      persistent
      max-width="600"
    >
      <template v-slot:activator="{ on, attrs }">
        <v-btn
          color="primary"
          dark
          v-bind="attrs"
          v-on="on"
        >
          Upload Products
        </v-btn>
      </template>
      <v-card>
        <v-card-title class="headline">
         Upload new products
        </v-card-title>
        <v-card-text>Select an excel file to upload your new products</v-card-text>
        <v-card-text class="pt-3"> <v-file-input
    v-model="files"
    color="deep-purple accent-4"
    counter
    label="File input"
    multiple
    placeholder="Select your files"
    outlined
    :show-size="1000"
  >
    <template v-slot:selection="{ index, text }">
      <v-chip
        v-if="index < 2"
        color="deep-purple accent-4"
        dark
        label
        small
      >
        {{ text }}
      </v-chip>

      <span
        v-else-if="index === 2"
        class="overline grey--text text--darken-3 mx-2"
      >
        +{{ files.length - 2 }} File(s)
      </span>
    </template>
  </v-file-input></v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="red darken-1"
            text
            @click="productsDialog = false"
          >
            Cancel
          </v-btn>
          <v-btn
            color="green darken-1"
            text
            @click="productsDialog = false"
          >
            Upload
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
      </v-row>
      <v-row>
         <v-data-table
    :headers="headers"
    :items="catalogueItems"
    sort-by="items"
    class="elevation-1"
    style="width:100%"
  >
  <template v-slot:item.status="{ item }">
      <v-chip
        :color="getColor(item.status)"
        dark
      >
        {{ item.status }}
      </v-chip>
    </template>
    <template v-slot:top>
        <v-dialog
      v-model="detailedInfoDialog"
      persistent
      max-width="600px"
    >
      <v-card>
          <v-system-bar
  height="30"
  v-if="editedItem.rejectionMessage != ''"
  color="red"
  class="justify-center"
><v-card-subtitle class="text-uppercase font-weight-bold white--text">Rejected</v-card-subtitle></v-system-bar>
        <v-card-text>
          <v-container>
             <v-card-title class="pl-0">
            <v-list-item-avatar class="ml-0" size="60">
                          <iframe :src="editedItem.image" width="100%" height="200px"></iframe>
                    </v-list-item-avatar>
                    <div>
                      <v-row
      align="center"
      justify="center"
      class="mb-2 ml-1"
    >
      <v-badge
        bordered
        color="success"
        icon="mdi-check"
        overlap
      >
        <v-btn
          class="white--text"
          color="primary"
          depressed
          small
          style="font-size:10px"
        >
          Fit for sale
        </v-btn>
      </v-badge>
       <div class="mx-1"></div>
      <v-badge
        bordered
        color="success"
        icon="mdi-check"
        overlap
      >
        <v-btn
          class="white--text"
          color="primary"
          depressed
          small
           style="font-size:10px"
        >
         Repeat Order
        </v-btn>
      </v-badge>
       <div class="mx-1"></div>
      <v-badge
        bordered
        color="success"
        icon="mdi-check"
        overlap
      >
        <v-btn
          class="white--text"
          color="primary"
          depressed
          small
           style="font-size:10px"
        >
          Export Compliant
        </v-btn>
      </v-badge>

      <div class="mx-0">
        </div>
        </v-row>
          <span class="font-weight-bold headline">{{editedItem.title}}</span>
                    </div>
        </v-card-title>
            <v-row>
               <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="Category"
                  :value="editedItem.category"
                  required></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="Sub Category"
                  :value="editedItem.subCategory"
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="Style Code"
                  :value="editedItem.styleCode"
                  required
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row>
               <v-col
                cols="12"
                sm="6"
                md="6"
              >
                <v-text-field
                  label="Stock (USD)"
                  :value="editedItem.price1"
                  required></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="6"
              >
                <v-text-field
                  label="Repeat Order (USD)"
                  :value="editedItem.price2"
                  required
                ></v-text-field>
              </v-col>
            </v-row>
             <v-row>
               <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="Quantity"
                  :value="editedItem.quantity"
                  required></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="Finish"
                  :value="editedItem.finish"
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="Ex-Factory (Max Days)"
                  :value="editedItem.maxExFactory"
                  required
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="12">
                <v-text-field
                  label="Image"
                  :value="editedItem.image"
                  required
                ></v-text-field>
              </v-col>
            </v-row>
            <v-expansion-panels>
    <v-expansion-panel
      v-for="(item,i) in editedItem.expansion"
      :key="i"
    >
      <v-expansion-panel-header>
        {{item.title}}
      </v-expansion-panel-header>
      <v-expansion-panel-content v-for="itemDetail in item.children" :key="itemDetail">
        <span class="font-weight-bold">{{itemDetail.title}}</span>: {{itemDetail.value}}
      </v-expansion-panel-content>
    </v-expansion-panel>
  </v-expansion-panels>
  <v-divider></v-divider>
  <div v-if="editedItem.rejectionMessage != ''">
  <v-card-title class="pl-0 pb-0 pt-8 red--text">Rejection Message</v-card-title>
  <v-card-title-subtitle class="black--text font-weight-normal">{{ editedItem.rejectionMessage}}</v-card-title-subtitle>
  </div>
          </v-container>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="blue darken-1"
            text
            @click="detailedInfoDialog = false"
          >
            Close
          </v-btn>
          <v-btn
            color="blue darken-1"
            text
            @click="detailedInfoDialog = false"
          >
            Save
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
        <v-dialog v-model="dialogDelete" max-width="500px">
          <v-card>
            <v-card-title class="headline">Are you sure you want to delete this item?</v-card-title>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="closeDelete">Cancel</v-btn>
              <v-btn color="blue darken-1" text @click="deleteItemConfirm">OK</v-btn>
              <v-spacer></v-spacer>
            </v-card-actions>
          </v-card>
        </v-dialog>
    </template>
    <template v-slot:item.actions="{ item }">
      <v-btn
        small
        class="mr-2"
        @click="editItem(item)"
      >
        View
      </v-btn>
    </template>
  </v-data-table>
      </v-row>
    </div>
  </v-container>
</div>
</template>

<script>
import sidebar from '../components/SideBar'
export default {
  name: 'Dashboard',
  components: {
    sidebar
  },
  data () {
    return {
      detailedInfoDialog: false,
      dialogDelete: false,
      productsDialog: false,
      headers: [
        {
          text: 'Product',
          align: 'start',
          sortable: false,
          value: 'title'
        },
        { text: 'Category', value: 'category' },
        { text: 'Sub Category', value: 'subCategory' },
        { text: 'Style Code', value: 'styleCode' },
        { text: 'Stock (USD)', value: 'price1' },
        { text: 'Repeat Order (USD)', value: 'price2' },
        { text: 'Status', value: 'status' },
        { text: 'Details', value: 'actions', sortable: false }
      ],
      catalogueItems: [
        { id: 1, title: 'Braided Round Rugs', categoryId: 3, subCategoryId: 18, category: 'Home Furnishing', subCategory: 'Floor Covering', styleCode: 'DI/RG/4700', price1: '7.45', price2: '8.05', image: 'https://drive.google.com/file/d/10wP91npAFp026qd3PjI7zsQiEuwveOi7/preview', status: 'Active', rejectionMessage: '' },
        { id: 2, title: 'Plated Lamp Shades', categoryId: 4, subCategoryId: 22, category: 'Hard Goods', subCategory: 'Lights', styleCode: 'Lamp Shades', price1: '16.88', price2: '20.25', image: 'https://drive.google.com/file/d/1fI1E7D7MW_L58GASHXCqRJ2ytN3tJi5b/preview', status: 'Active', rejectionMessage: '' },
        { id: 3, title: 'Tray Set of 3', categoryId: 3, subCategoryId: 15, category: 'Hard Goods', subCategory: 'Kitchen and Dining', styleCode: '266417', price1: '52.90', price2: '63.06', image: 'https://drive.google.com/file/d/1iP4WeAYB7OElSIl5SWiygL9pFagiCOut/preview', status: 'Active', rejectionMessage: '' },
        {
          id: 4,
          title: 'Iron bowl',
          category: 'Hard Goods',
          subCategory: 'Table Top',
          categoryId: 5,
          subCategoryId: 32,
          styleCode: 'RST-STOCK',
          price1: '2.50',
          price2: '3.38',
          quantity: '10,000',
          finish: 'Mint Green',
          maxExFactory: '22 to 30 days',
          lables: 'Can be done',
          fitForSale: 'Yes',
          repeatOrders: 'Yes',
          expansion: [
            {
              title: 'Sizing Parameters',
              children: [
                { title: 'Size (cm)', value: '15x15x7' },
                { title: 'Inner Dimensions (cm)', value: '17.5X17.5X8.5' },
                { title: 'Piece Packing Weight', value: '0.37' }
              ]
            },
            {
              title: 'Repeat Order Information',
              children: [
                { title: 'Lead Time (Ex-India - Days)', value: '45' },
                { title: 'Repeat Order MOQ', value: '500' }
              ]
            },
            {
              title: 'Additional Information',
              children: [
                { title: 'Payment Terms', value: '50% advance after initial inspection and balance after Final inspection' }
              ]
            }
          ],
          image: 'https://drive.google.com/file/d/1JRSjseAq-REKWSXdnrrP8ehpQDsCakLD/preview',
          status: 'Waiting Approval',
          rejectionMessage: ''
        },
        {
          id: 5,
          title: 'Silk Check Cushion Cover',
          category: 'Home Furnishing',
          subCategory: 'Decoration',
          categoryId: 4,
          subCategoryId: 17,
          styleCode: 'Silk',
          price1: '4.35',
          price2: '9.11',
          quantity: '50 Assorted',
          finish: 'N/A',
          maxExFactory: '5 to 7 days',
          lables: 'Can be done',
          fitForSale: 'Yes',
          repeatOrders: 'Yes',
          expansion: [
            {
              title: 'Sizing Parameters',
              children: [
                { title: 'Size (cm)', value: '40x40' },
                { title: 'Inner Dimensions (cm)', value: '50x50x40' },
                { title: 'Piece Packing Weight', value: '10' }
              ]
            },
            {
              title: 'Repeat Order Information',
              children: [
                { title: 'Lead Time (Ex-India - Days)', value: '120' },
                { title: 'Repeat Order MOQ', value: '300' }
              ]
            },
            {
              title: 'Additional Information',
              children: [
                { title: 'Payment Terms', value: '50% advance after initial inspection and balance after Final inspection' }
              ]
            }
          ],
          image: 'https://drive.google.com/file/d/1-M1MVlEdLLKBlmWzLhmX192yF7AD-uSb/preview',
          status: 'Rejected',
          rejectionMessage: 'Please fill in your product finish'
        }
      ],
      editedIndex: -1,
      editedItem: {
        id: 0,
        title: '',
        categoryId: 0,
        subCategoryId: 0,
        styleCode: '',
        price1: '',
        price2: '',
        quantity: '',
        finish: '',
        size: '',
        maxExFactory: '',
        lables: '',
        fitForSale: '',
        repeatOrders: '',
        additionalInformation: '',
        innerDimensions: '',
        piecePackingWeight: '',
        ROLeadTime: '',
        RoMOQ: '',
        paymentTerms: '',
        exportCompliance: '',
        image: '',
        status: '',
        expansion: [],
        rejectionMessage: ''
      },
      defaultItem: {
        name: '',
        calories: 0,
        fat: 0,
        carbs: 0,
        protein: 0
      }
    }
  },
  computed: {
    formTitle () {
      return this.editedIndex === -1 ? 'New Item' : 'Edit Item'
    }
  },

  watch: {
    dialog (val) {
      val || this.close()
    },
    dialogDelete (val) {
      val || this.closeDelete()
    }
  },

  methods: {
    editItem (item) {
      this.editedIndex = this.catalogueItems.indexOf(item)
      this.editedItem = Object.assign({}, item)
      this.detailedInfoDialog = true
    },

    deleteItem (item) {
      this.editedIndex = this.catalogueItems.indexOf(item)
      this.editedItem = Object.assign({}, item)
      this.dialogDelete = true
    },

    deleteItemConfirm () {
      this.desserts.splice(this.editedIndex, 1)
      this.closeDelete()
    },

    close () {
      this.detailedInfoDialog = false
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem)
        this.editedIndex = -1
      })
    },

    closeDelete () {
      this.dialogDelete = false
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem)
        this.editedIndex = -1
      })
    },

    save () {
      if (this.editedIndex > -1) {
        Object.assign(this.desserts[this.editedIndex], this.editedItem)
      } else {
        this.desserts.push(this.editedItem)
      }
      this.close()
    },

    getColor (status) {
      if (status === 'Waiting Approval') return 'orange'
      else if (status === 'Rejected') return 'red'
      else return 'green'
    }
  }
}
</script>
