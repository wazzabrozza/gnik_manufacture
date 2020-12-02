<template>
<v-main>
      <v-container >
        <v-row class="justify-center">
          <v-col cols="2">
            <v-card outlined>
            <v-card-title>Filters</v-card-title>
            <v-divider></v-divider>
            <template>
              <v-treeview :items="items" :open.sync="open" :active.sync="active" :selected-color="'#fff'" activatable open-on-click dense></v-treeview>
            </template>
            <v-divider></v-divider>
            <v-card-title>Price</v-card-title>
            <v-range-slider
              v-model="range"
              :max="max"
              :min="min"
              :height="10"
              class="align-center"
              dense
            ></v-range-slider>
            <v-row class="pa-2" dense>
              <v-col cols="12" sm="5">
                <v-text-field
                  :value="range[0]"
                  label="Min"
                  outlined
                  dense
                  @change="$set(range, 0, $event)"
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="2">
                <p class="pt-2 text-center">TO</p>
              </v-col>
              <v-col cols="12" sm="5">
                <v-text-field
                  :value="range[1]"
                  label="Max"
                  outlined
                  dense
                  @change="$set(range, 1, $event)"
                ></v-text-field>
              </v-col>
            </v-row>
            <v-divider></v-divider>
            <v-card-title class="pb-0">Customer Rating</v-card-title>
            <v-container class="pt-0"  fluid>
              <v-checkbox append-icon="mdi-star" label="4 & above" hide-details dense></v-checkbox>
              <v-checkbox append-icon="mdi-star" label="3 & above" hide-details dense></v-checkbox>
              <v-checkbox append-icon="mdi-star" label="2 & above" hide-details dense></v-checkbox>
              <v-checkbox append-icon="mdi-star" label="1 & above" hide-details dense></v-checkbox>
            </v-container>
            <v-divider></v-divider>
            <v-card-title class="pb-0">Size</v-card-title>
            <v-container class="pt-0" fluid>
              <v-checkbox  label="XS" hide-details dense></v-checkbox>
              <v-checkbox  label="S" hide-details dense></v-checkbox>
              <v-checkbox  label="M" hide-details dense></v-checkbox>
              <v-checkbox  label="L" hide-details dense></v-checkbox>
              <v-checkbox  label="XL" hide-details dense></v-checkbox>
              <v-checkbox  label="XXL" hide-details dense></v-checkbox>
              <v-checkbox  label="XXXL" hide-details dense></v-checkbox>
            </v-container>

          </v-card>
          </v-col>

          <v-col class="col-7">
             <div>
               <v-tabs
      color="deep-purple accent-4"
      right
    >
     <v-card-title>
       Catalogue Items
       <v-badge
        v-if="this.active == 34"
        inline
        :content="this.catalogueSearch.length"
      ></v-badge>
      <v-badge
        v-else
        inline
        :content="this.selectedCategory.length"
      ></v-badge>
      <v-text-field
        class="pl-10 pt-0 mt-0"
        v-model="search"
        append-icon="mdi-magnify"
        label="Search products, style codes"
        single-line
        hide-details
      ></v-text-field>
    </v-card-title>
      <v-spacer></v-spacer>
      <v-tab>List View</v-tab>
      <v-tab>Card View</v-tab>
      <v-tab-item class="pt-5">
             <v-card>
              <v-list two-line v-if="this.active != 34">
                <div v-if="this.selectedCategory.length == 0">
                 <v-card-title class="text-center">No Products</v-card-title>
               </div>
                <template v-for="item in selectedCategory" class="d-flex">
                  <v-list-item
                    :key="item.id"
                    class="justify-space-between">
                   <div class="d-flex">
                      <v-list-item-avatar>
                          <iframe :src="item.image" width="100%" height="150px"></iframe>
                    </v-list-item-avatar>
                    <v-list-item-content>
                      <v-list-item-title>{{ item.title }}</v-list-item-title>

                      <v-list-item-subtitle>
                        {{item.styleCode}}
                      </v-list-item-subtitle>
                    </v-list-item-content>
                  </div>
                  <div>
                     <v-list-item-content>
                      <v-list-item-subtitle>Stock (USD)</v-list-item-subtitle>
                      <v-list-item-title>${{ item.price1 }}</v-list-item-title>
                    </v-list-item-content>
                  </div>
                   <div>
                     <v-list-item-content>
                      <v-list-item-subtitle>Repeat Order (USD) </v-list-item-subtitle>
                      <v-list-item-title>${{ item.price2 }}</v-list-item-title>
                    </v-list-item-content>
                  </div>
                   <div>
                     <v-list-item-content>
                          <v-row
                          align="center"
                          class="mx-0"
                        >
                          <v-rating
                            :value="4.5"
                            color="amber"
                            dense
                            half-increments
                            readonly
                            size="14"
                          ></v-rating>

                          <div class="grey--text ml-4">
                            4.5 (413)
                          </div>
                        </v-row>
                    </v-list-item-content>
                  </div>
                     <div>
                     <v-list-item-content>
                        <v-btn
        color="deep-purple"
        text
      >
        View
      </v-btn>
                    </v-list-item-content>
                  </div>
                  </v-list-item>
                </template>
              </v-list>
                 <div v-else>
                   <v-list two-line>
                <template v-for="item in catalogueSearch" class="d-flex">
                  <v-list-item
                    :key="item.id"
                    class="justify-space-between"
                  >
                   <div class="d-flex justify-space-evenly">
                      <v-list-item-avatar>
                          <iframe :src="item.image" width="100%" height="150px"></iframe>
                    </v-list-item-avatar>
                    <v-list-item-content>
                      <v-list-item-title>{{ item.title }}</v-list-item-title>

                      <v-list-item-subtitle>
                        {{item.styleCode}}
                      </v-list-item-subtitle>
                    </v-list-item-content>
                  </div>
                  <div>
                     <v-list-item-content>
                      <v-list-item-subtitle>Stock (USD)</v-list-item-subtitle>
                      <v-list-item-title>${{ item.price1 }}</v-list-item-title>
                    </v-list-item-content>
                  </div>
                   <div>
                     <v-list-item-content>
                      <v-list-item-subtitle>Repeat Order (USD) </v-list-item-subtitle>
                      <v-list-item-title>${{ item.price2 }}</v-list-item-title>
                    </v-list-item-content>
                  </div>
                   <div>
                     <v-list-item-content>
                          <v-row
                          align="center"
                          class="mx-0"
                        >
                          <v-rating
                            :value="4.5"
                            color="amber"
                            dense
                            half-increments
                            readonly
                            size="14"
                          ></v-rating>

                          <div class="grey--text ml-4">
                            4.5 (413)
                          </div>
                        </v-row>
                    </v-list-item-content>
                  </div>
                     <div>
                     <v-list-item-content>
                        <v-btn
        color="deep-purple"
        text
      >
        View
      </v-btn>
                    </v-list-item-content>
                  </div>
                  </v-list-item>
                </template>
              </v-list>
                </div>
            </v-card>
        </v-tab-item>
        <v-tab-item class="pt-5">
             <div class="">
               <div v-if="this.active != 34" class="d-flex flex-wrap">
                   <div v-if="this.selectedCategory.length == 0">
                 <v-card-title>No products</v-card-title>
               </div>
               <v-col v-for="item in catalogueSearch && selectedCategory"
    :key="item.id">
        <v-card>

    <!--<v-img
      height="250"
      src="https://drive.google.com/file/d/10wP91npAFp026qd3PjI7zsQiEuwveOi7/preview"
    ></v-img>-->
    <iframe :src="item.image" width="100%" height="150px"></iframe>
    <v-card-title>{{item.title}}</v-card-title>
    <v-card-subtitle>{{item.styleCode}}</v-card-subtitle>
     <v-card-title class="pt-0">
        ${{item.price1}}
      </v-card-title >

       <v-card-subtitle class="pt-0">
      <v-row
        align="center"
        class="mx-0"
      >
        <v-rating
          :value="4.5"
          color="amber"
          dense
          half-increments
          readonly
          size="14"
        ></v-rating>

        <div class="grey--text ml-4">
          4.5 (413)
        </div>
      </v-row>
        </v-card-subtitle >

    <v-divider class="mx-4"></v-divider>

    <v-card-actions>
      <v-btn
        color="deep-purple"
        text
      >
        View
      </v-btn>
    </v-card-actions>
  </v-card></v-col></div><div v-else class="d-flex flex-wrap">
    <v-col
      v-for="item in catalogueItems && catalogueSearch"
    :key="item.id">
        <v-card>
    <!--<v-img
      height="250"
      src="https://drive.google.com/file/d/10wP91npAFp026qd3PjI7zsQiEuwveOi7/preview"
    ></v-img>-->
    <iframe :src="item.image" width="100%" height="150px"></iframe>
    <v-card-title>{{item.title}}</v-card-title>
    <v-card-subtitle>{{item.styleCode}}</v-card-subtitle>
     <v-card-title class="pt-0">
        ${{item.price1}}
      </v-card-title >

       <v-card-subtitle class="pt-0">
      <v-row
        align="center"
        class="mx-0"
      >
        <v-rating
          :value="4.5"
          color="amber"
          dense
          half-increments
          readonly
          size="14"
        ></v-rating>

        <div class="grey--text ml-4">
          4.5 (413)
        </div>
      </v-row>
        </v-card-subtitle >

    <v-divider class="mx-4"></v-divider>

    <v-card-actions>
      <v-btn
        color="deep-purple"
        text
      >
        View
      </v-btn>
    </v-card-actions>
  </v-card>
    </v-col>
               </div>
      </div>
        </v-tab-item>
    </v-tabs>
            </div>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
</template>

<script>
export default {
  data: () => ({
    selectedItem: 0,
    search: '',
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
      { text: 'Price 1', value: 'price1' },
      { text: 'Price 2', value: 'price2' }
    ],
    catalogueItems: [
      { id: 1, title: 'Braided Round Rugs', categoryId: 3, subCategoryId: 18, category: 'Home Furnishing', subCategory: 'Floor Covering', styleCode: 'DI/RG/4700', price1: '7.45', price2: '8.05', image: 'https://drive.google.com/file/d/10wP91npAFp026qd3PjI7zsQiEuwveOi7/preview', status: 'Active' },
      {
        id: 2,
        title: 'Plated Lamp Shades',
        categoryId: 4,
        subCategoryId: 22,
        category: 'Hard Goods',
        subCategory: 'Lights',
        styleCode: 'Lamp Shades',
        price1: '16.88',
        price2: '20.25',
        quantity: 'N/A',
        finish: 'N/A',
        maxExFactory: '16 to 21 days',
        lables: 'Can be done',
        fitForSale: 'Yes',
        repeatOrders: 'Yes',
        expansion: [
          {
            title: 'Sizing Parameters',
            children: [
              { title: 'Size (inch)', value: 'N/A' },
              { title: 'Inner Dimensions (inch)', value: '20' },
              { title: 'Piece Packing Weight', value: '7.5' }
            ]
          },
          {
            title: 'Repeat Order Information',
            children: [
              { title: 'Lead Time (Ex-India - Days)', value: '75' },
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
        image: 'https://drive.google.com/file/d/1fI1E7D7MW_L58GASHXCqRJ2ytN3tJi5b/preview',
        status: 'Active'
      },
      {
        id: 3,
        title: 'Tray Set of 3',
        categoryId: 3,
        subCategoryId: 15,
        category: 'Hard Goods',
        subCategory: 'Kitchen and Dining',
        styleCode: '266417',
        price1: '52.90',
        price2: '63.06',
        quantity: '150',
        finish: 'N/A',
        maxExFactory: '22 to 30 days',
        lables: 'Can be done',
        fitForSale: 'Yes',
        repeatOrders: 'Yes',
        expansion: [
          {
            title: 'Sizing Parameters',
            children: [
              { title: 'Size (inch)', value: '25.5' },
              { title: 'Inner Dimensions (inch)', value: '26.5x18x4.5' },
              { title: 'Piece Packing Weight', value: '1' }
            ]
          },
          {
            title: 'Repeat Order Information',
            children: [
              { title: 'Lead Time (Ex-India - Days)', value: '75' },
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
        image: 'https://drive.google.com/file/d/1iP4WeAYB7OElSIl5SWiygL9pFagiCOut/preview',
        status: 'Active'
      },
      {
        id: 4,
        title: 'Cushion Cover',
        category: 'Home Furnishing',
        subCategory: 'Decoration',
        categoryId: 4,
        subCategoryId: 17,
        styleCode: 'Foil Prints',
        price1: '2.00',
        price2: '2.57',
        quantity: '350',
        finish: 'Assorted',
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
              { title: 'Repeat Order MOQ', value: '300 Per Colour' }
            ]
          },
          {
            title: 'Additional Information',
            children: [
              { title: 'Payment Terms', value: '50% advance after initial inspection and balance after Final inspection' }
            ]
          }
        ],
        image: 'https://drive.google.com/file/d/1oYoNWahqO2FBBxg0C04qOsWv73Dm5yzK/preview',
        status: 'Active'
      }
    ],
    range: [0, 1000],
    select: 'Popularity',
    options: [
      'Default',
      'Popularity',
      'Relevance',
      'Price: Low to High',
      'Price: High to Low'
    ],
    page: 1,
    items: [
      {
        id: 34,
        name: 'All'
      },
      {
        id: 2,
        name: 'Garments',
        children: [
          { id: 1, name: 'Kids' },
          { id: 2, name: 'Men' },
          { id: 3, name: 'Women' },
          { id: 4, name: 'Baby Bedding and Clothing' }
        ]
      },
      {
        id: 3,
        name: 'Accessories',
        children: [
          { id: 5, name: 'Candles' },
          { id: 6, name: 'Christams Ornaments' },
          { id: 7, name: 'Fragrance' },
          { id: 8, name: 'Bags' },
          { id: 9, name: 'Candles' },
          { id: 10, name: 'Essentail Oils and Fragrances' },
          { id: 11, name: 'Incenses' },
          { id: 12, name: 'Jewellery' },
          { id: 13, name: 'Scarfs' }
        ]
      },
      {
        id: 4,
        name: 'Home Furnishing',
        children: [
          { id: 14, name: 'Bath' },
          { id: 15, name: 'Kitchen' },
          { id: 16, name: 'Bedding' },
          { id: 17, name: 'Decoration' },
          { id: 18, name: 'Floor Covering' },
          { id: 19, name: 'Table Linen' }
        ]
      },
      {
        id: 5,
        name: 'Hard Goods',
        children: [
          { id: 20, name: 'Decor' },
          { id: 21, name: 'Decor and Storage' },
          { id: 22, name: 'Decoration' },
          { id: 23, name: 'Tableware' },
          { id: 24, name: 'Decoration and Utility' },
          { id: 25, name: 'Kitchen and Dining Products' },
          { id: 26, name: 'Storage' },
          { id: 27, name: 'Furniture' },
          { id: 28, name: 'Garden' },
          { id: 29, name: 'Lights' },
          { id: 30, name: 'Mirrors' },
          { id: 31, name: 'Storage' },
          { id: 32, name: 'Table Top' },
          { id: 33, name: 'Wall Decor' }
        ]
      }
    ],
    min: 0,
    max: 1000,
    active: [34],
    open: []
  }),
  computed: {
    catalogueSearch: function () {
      return this.catalogueItems.filter(item => {
        var price = item.price1 >= this.range[0] && item.price1 <= this.range[1]
        var search = item.title.toLowerCase().includes(this.search.toLowerCase()) || item.styleCode.toLowerCase().includes(this.search.toLowerCase())
        return price && search
      })
    },
    selectedCategory: function () {
      // const openId = this.open[0]
      const activeId = this.active[0]
      return this.catalogueItems.filter(item => item.subCategoryId === activeId)
    }
  }
}
</script>

<style scoped>
.justify-space-evenly {
  box-sizing: border-box;
  width: 250px;
}
</style>
