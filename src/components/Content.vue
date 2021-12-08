<template>
    <div class="container">
        <div class="row mt-5">

            <!-- FORM DIV CONTAINER -->
            <div class="col-sm-4">
                <div class="card">
                    <div class="card-header">
                        <h3>Add aproduct</h3>
                    </div>
                    <div class="card-body">
                        <form v-on:submit.prevent="addProduct">
                            <div class="form-group p-2">
                                <input
                                    type="text"
                                    class="form-control"
                                    placeholder="New product"
                                    v-model="name"
                                >
                            </div>
                            <div class="form-group p-2">
                                <input
                                    type="text"
                                    class="form-control"
                                    placeholder="Amount"
                                    v-model="amount"
                                >
                            </div>
                            <div class="form-group p-2">
                                <input 
                                    type="text"
                                    class="form-control"
                                    placeholder="Unit price"
                                    v-model="unitPrice"
                                >
                                <div class="form-group p-2">
                                    <button class="btn btn-success" type="submit">Add product</button>
                                </div>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
            <!-- END OF FORM DIV -->

            <!-- TABLE DATA CONTAINER -->
            <div class="col-sm-8">
                <div class="card">
                    <div class="card-header">
                        <h3>Carshop</h3>
                    </div>
                    <div class="card-body">
                        <table class="table">
                            <thead>
                                <tr>
                                    <th scope="col">Name of product</th>
                                    <th scope="col">Amount</th>
                                    <th scope="col">Unit Price</th>
                                    <th scope="col">Subtotal</th>
                                    <th scope="col">Total</th>
                                    <th scope="col">Actions</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="(product, index) in products" :key="product.id">
                                    <td>
                                        <span v-if="formUpdate && idUpdate == index">
                                            <div class="form-group">
                                                <input
                                                    type="text"
                                                    class="form-control"
                                                    v-model="newName"
                                                >
                                            </div>
                                        </span>
                                        <span v-else>
                                            {{product.name}}
                                        </span>
                                    </td>
                                    <td>
                                        <span v-if="formUpdate && idUpdate == index">
                                            <div class="form-group">
                                                <input 
                                                    type="text"
                                                    class="form-control"
                                                    v-model="newAmount"
                                                >
                                            </div>
                                        </span>
                                        <span v-else>
                                            {{product.amount}}
                                        </span>
                                    </td>
                                    <td>
                                        <span v-if="formUpdate && idUpdate == index">
                                            <div class="form-group">
                                                <input 
                                                    type="text"
                                                    class="form-control"
                                                    v-model="newUnitPrice"
                                                >
                                            </div>
                                        </span>
                                        <span v-else>
                                            {{product.unitPrice}}
                                        </span>
                                    </td>
                                    <td>{{subtotalOfProduct(product.amount, product.unitPrice)}}</td>
                                    <td>{{totalAll(product.amount, product.unitPrice)}}</td>
                                    <td>
                                        <span v-if="formUpdate && idUpdate == index">
                                        <div class="actions">
                                            <button 
                                                class="btn btn-success"
                                                v-on:click="updateProduct(index)"
                                            >Upgrade</button>
                                        </div>
                                        </span>
                                        <span v-else>
                                            <td>
                                                <button
                                                    class="btn btn-warning"
                                                    v-on:click="editProduct(index)"
                                                >
                                                    Editar
                                                </button>
                                                <button
                                                    class="btn btn-danger"
                                                    v-on:click="removeProduct(index)"
                                                >
                                                    Eliminar
                                                </button>
                                            </td>
                                        </span>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
            <!-- END OF TABLE DATA CONTAINER -->

        </div>
    </div>
</template>

<script>

export default {
    name: "Content",
    data() {
        return {
            name: "",
            amount: null,
            unitPrice: null,
            formUpdate: false,
            idUpdate: -1,
            newName: "",
            newAmount: null,
            newUnitPrice: null,
            products: []
        }
    },
    methods: {
        addProduct() {
            this.products.push({
                id: +new Date(),
                name: this.name,
                amount: this.amount,
                unitPrice: this.unitPrice
            })
            this.name = ""
            this.amount = null
            this.unitPrice = null
        },

        removeProduct(product) {
            alert('Product deleted')
            this.products.splice(product, 1)
        },

        editProduct(product) {
            this.idUpdate = product
            this.newName = this.products[product].name
            this.newAmount = this.products[product].amount
            this.newUnitPrice = this.products[product].unitPrice
            this.formUpdate = true;
        },

        updateProduct(product) {
            alert('Product updated')
            this.formUpdate = false
            this.products[product].name = this.newName
            this.products[product].amount = this.newAmount
            this.products[product].unitPrice = this.newUnitPrice
        },

        subtotalOfProduct(amount, unitPrice) {
            return amount * unitPrice
        },

        iva(amount, unitPrice) {
            let allPorcent = 100
            let iva = 16
            let subtotal = amount * unitPrice * iva
            let total = subtotal / allPorcent
            return total
        },

        totalAll(amount, unitPrice) {
            return this.iva(amount, unitPrice) + this.subtotalOfProduct(amount, unitPrice)
        }
    }
}
</script>

<style>

    button {
        padding: 5px;
        margin: 5px;
    }
</style>
