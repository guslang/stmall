<template>

    <v-data-table
        :headers="headers"
        :items="searchOrderedProduct"
        :items-per-page="5"
        class="elevation-1"
    ></v-data-table>

</template>

<script>
    const axios = require('axios').default;

    export default {
        name: 'SearchOrderedProductView',
        props: {
            value: Object,
            editMode: Boolean,
            isNew: Boolean
        },
        data: () => ({
            headers: [
                { text: "id", value: "id" },
            ],
            searchOrderedProduct : [],
        }),
          async created() {
            var temp = await axios.get(axios.fixUrl('/searchOrderedProducts'))

            temp.data._embedded.searchOrderedProducts.map(obj => obj.id=obj._links.self.href.split("/")[obj._links.self.href.split("/").length - 1])

            this.searchOrderedProduct = temp.data._embedded.searchOrderedProducts;
        },
        methods: {
        }
    }
</script>

