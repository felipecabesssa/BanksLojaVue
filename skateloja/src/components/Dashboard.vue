<template>
    <div id="skate-table">
        <div>
            <div id="skate-table-heading">
                <div>Cliente: </div>
                <div id="imgMenu"><img src="/img/icons/shape.png" alt=""></div>
                <div id="imgMenu"><img src="/img/icons/truck.png" alt=""></div>
                <div id="imgMenu"><img src="/img/icons/roda.png" alt=""></div>
                <div id="imgMenu"><img src="/img/icons/rolamento.png" alt=""></div>
                <div id="imgMenu"><img src="/img/icons/opcionais.png" alt=""></div>
                <div>Ações: </div>
            </div>
        </div>

        <div id="skate-table-rows">
            <div class="skate-table-row" v-for="pedido in pedidos" :key="pedido.id" >
                <div>{{ pedido.nome }}</div>
                <div>{{ pedido.shape }}</div>
                <div>{{ pedido.truck }}</div>
                <div>{{ pedido.roda }}</div>
                <div>{{ pedido.rolamento }}</div>
                <div>
                    <ul>
                        <li v-for="(opcional, index) in pedido.opcionais" :key="index">
                            {{ opcional }}
                        </li>
                    </ul>
                </div>
                <div>
                    <select name="status" class="status">
                        <option value="">Status</option>
                        <option v-for="s in status" :key="s.id" value="s.tipo" :selected="pedido.status == s.tipo">
                            {{ s.tipo }}
                        </option>
                    </select>
                    <button class="delete-btn" @click="deletePedido(pedido.id)">Cancelar</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Dashboard",
    data() {
        return {
            pedidos: null,
            skate_id: null,
            status: []
        }
    },
    methods: {
        async getPedidos() {

            const request = await fetch("http://localhost:3000/pedidos");

            const data = await request.json();

            this.pedidos = data;

            console.log(this.pedidos);

            //resgatar os status
            this.getStatus();

        },
        async getStatus() {

            const request = await fetch("http://localhost:3000/status");

            const data = await request.json();

            this.status = data;

        },
        async deletePedido(id) {

            const request = await fetch(`http://localhost:3000/pedidos/${id}`, { 
                method: "DELETE"
            });

            const response = await request.json();

            //msg

            this.getPedidos();

        }
    },
    mounted() {
        this.getPedidos();
    }
}
</script>


<style scoped>
    .container {
        width: 500px;
        margin-left: -45px;
    }
    #imgMenu img {
        width: 50px;
        height: 50px;
    }
    #skate-table {
        max-width: 1200px;
        margin: 0 auto;
    }
    #skate-table-heading,
    #skate-table-rows,
    .skate-table-row {
        display: flex;
        flex-wrap: wrap;
        font-size: 10px;
    }
    #skate-table-heading {
        font-size: 12px;
        font-weight: bold;
        padding: 2px;
        border-bottom: 3px solid #333;
    }
    #skate-table-heading div,
    .skate-table-row div {
        width: 14%;
    }
    .skate-table-row {
        width: 100%;
        padding: 2px;
        border-bottom: 1px solid #ccc;
    }
    #skate-table-heading .order-id,
    .skate-table-row .order-number {
        width: 3%;
    }
    select {
        font-size: 8px;
        padding: 2px 3px;
        margin-right: 5px;
    }
    .delete-btn {
        width: 80px;
        background-color: #222;
        color: #FCBA03;
        font-weight: bold;
        border: 2px solid #222;
        padding: 3px;
        font-size: 8px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
    }
    .delete-btn:hover {
        background-color: transparent;
        color: #222;
    }
    @media(min-width:770px) {
        .container {
        width: 1200px;
        margin: 0 auto;
        }

        #imgMenu img {
            width: 100px;
            height: 100px;
        }

        #skate-table-heading,
        #skate-table-rows,
        .skate-table-row {
            font-size: 14px;
            padding-top: 7px;
        }

        .delete-btn {
        padding: 5px;
        font-size: 14px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
        }

        select {
        font-size: 14px;
        padding: 5px 10px;
        margin-right: 5px;
        }

        #skate-table-heading {
        font-size: 18px;
        padding: 5px;
    }
    }
</style>