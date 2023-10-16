<template>
<div class="container">
    <div class="row d-flex justify-content-center mt-3 pt-3">
        <div class="col-sm-8">
            <h1 class="text-success">Mi caja registradora</h1>
        </div>
    </div>
    <div class="row mt-3 pt-3">
        <!--Formulario-->
        <div class="col-sm-6">
            <div>
                <div class="mb-3">
                    <label class="form-label">Nombres</label>
                    <input v-model="nombres" type="text" class="form-control" >
                </div>
                <div class="mb-3">
                    <label class="form-label">Apellidos</label>
                    <input v-model="apellidos" type="text" class="form-control" >
                </div>
                <div class="mb-3">
                    <label class="form-label">Productos</label>
                    <select v-model="id_seleccionado" class="form-control" @change="comprobar()">
                        <option v-for="producto in productos" :key="producto.id" :value="producto.id">
                            {{ producto.nombre }}
                        </option>
                    </select>
                </div>
                <div class="mb-3">
                    <label class="form-label">Cantidad</label>
                    <input v-model="cantidad" type="number" class="form-control" >
                </div>
                <button @click="agregar()" class="btn btn-primary">Agregar</button>
            </div>
        </div>
        <!--End Formulario-->
        <!--Resultado-->
        <div class="col-sm-6">
            <h5 class="mb-2">Lista de compra</h5>
            <p>{{ nombres }}  {{ apellidos }}</p>
            <div class="mt-3">
                <table class="table table-bordered">
                    <thead>
                        <tr>
                            <td>Producto</td>
                            <td>Cantidad</td>
                            <td>Valor</td>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(comprado,index) in comprados" :key="index">
                            <td>{{ comprado.producto }}</td>
                            <td>{{ comprado.cantidad }}</td>
                            <td align="right">{{ comprado.valor }}</td>
                        </tr>
                        <tr>
                            <td colspan="2">Subtotal</td>
                            <td align="right">{{ subtotal }}</td>
                        </tr>
                        <tr>
                            <td colspan="2">IVA</td>
                            <td align="right">{{ iva }}</td>
                        </tr>
                        <tr>
                            <td colspan="2">Valor Total</td>
                            <td align="right">{{ valor_total }}</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
        <!--End Resultado-->
    </div>
</div>
</template>

<script>

export default {
    name:'CajaApp',
    data() {
        return {
            nombres:'',
            apellidos: '',
            cantidad: 1,
            productos: [
                {
                    "id": 1,
                    "nombre":"Producto 1",
                    "valor": 10000
                },
                {
                    "id": 2,
                    "nombre":"Producto 2",
                    "valor": 20000
                },
                {
                    "id": 3,
                    "nombre":"Producto 3",
                    "valor": 5000
                },
                {
                    "id": 4,
                    "nombre":"Producto 4",
                    "valor": 1000
                }
            ],
            id_seleccionado:1,
            comprados: []
        }
    },
    computed : {
        seleccionado() {
            return this.productos.find((element) => element.id == this.id_seleccionado)
        },
        valor_producto() {
            return this.seleccionado.valor * this.cantidad
        },
        subtotal() {
            let subtotal = 0;
            this.comprados.forEach(element => {
                subtotal = subtotal + element.valor
            });
            return subtotal
        },
        iva() {
            let iva = this.subtotal * 0.19
            return iva.toFixed(0)
        },
        valor_total(){
            let total = parseFloat(this.subtotal) + parseFloat(this.iva)
            return total
        }
    },
    methods: {
        comprobar() {
            console.log(this.seleccionado)
            // console.log('valor_producto', this.valor_producto)
        },
        agregar() {
            let comprado = {
                producto: this.seleccionado.nombre,
                valor: this.valor_producto,
                cantidad: this.cantidad
            }
            this.comprados.push(comprado)
            // console.log(this.comprados)
        }
    }
}

</script>

<style lang="scss" scoped>

</style>