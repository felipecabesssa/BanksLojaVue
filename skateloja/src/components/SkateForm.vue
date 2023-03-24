<template>
    <div>
        <Message :msg="msg" v-show="msg" />
        <div>
            <form id="skate-form" @submit="createSkate">

                <div class="input-container">
                    <label for="nome">Nome do cliente</label>
                    <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite seu nome: ">
                </div>

                <div class="input-container">
                    <label for="shape">Escolha o shape:</label>
                    <select name="shape" id="shape" v-model="shape">
                        <option value="">Selecione o shape</option>
                        <option v-for="shape in shapes" :key="shape.id" :value="shape.tipo">{{ shape.tipo }}</option>
                    </select>
                </div>

                <div class="input-container">
                    <label for="truck">Escolha o truck:</label>
                    <select name="truck" id="truck" v-model="truck">
                        <option value="">Selecione o truck</option>
                        <option v-for="truck in trucks" :key="truck.id" :value="truck.tipo">{{ truck.tipo }}</option>
                    </select>
                </div>

                <div class="input-container">
                    <label for="roda">Escolha a roda:</label>
                    <select name="roda" id="roda" v-model="roda">
                        <option value="">Selecione o roda</option>
                        <option v-for="roda in rodas" :key="roda.id" :value="roda.tipo">{{ roda.tipo }}</option>
                    </select>
                </div>

                <div class="input-container">
                    <label for="rolamento">Escolha o rolamento:</label>
                    <select name="rolamento" id="rolamento" v-model="rolamento">
                        <option value="">Selecione o rolamento</option>
                        <option v-for="rolamento in rolamentos" :key="rolamento.id" :value="rolamento.tipo">{{ rolamento.tipo }}</option>
                    </select>
                </div>

                <div id="opcionais-container" class="input-container">
                    <label for="opcionais">Selecione os opcionais:</label>
                    <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id" >
                        <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
                        <span>{{ opcional.tipo }}</span>
                    </div>
                    
                </div>

                <div class="input-container">
                    <input type="submit" class="submit-btn" value="Montar meu carrinho">
                </div>
            </form>
        </div>
    </div>
</template>

<script>
import Message from './Message.vue';
export default {
  components: { Message },
    name: "SkateForm",
    data() {
        return {
            shapes: null,
            trucks: null,
            rodas: null,
            rolamentos: null,
            opcionaisdata: null,
            nome: null,
            shape: null,
            truck: null,
            roda: null,
            rolamento: null,
            opcionais: [],
            msg: null
        }
    },
    methods: {
        async getPecas() {

            const req = await fetch("http://localhost:3000/skates");
            const data = await req.json();

            this.shapes = data.shapes;
            this.trucks = data.trucks;
            this.rodas = data.rodas;
            this.rolamentos = data.rolamentos;
            this.opcionaisdata = data.opcionais;

        },
        async createSkate(e){

            e.preventDefault();

            const data = {
                nome: this.nome,
                shape: this.shape,
                truck: this.truck,
                roda: this.roda,
                rolamento: this.rolamento,
                opcionais: Array.from(this.opcionais),
                status: "Solicitado"

            }

            const dataJson = JSON.stringify(data);

            const request = await fetch("http://localhost:3000/pedidos", {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: dataJson
            });

            const response = await request.json();

            // colocar msg de sistema
            this.msg = `Pedido Nº ${response.id} realizado com sucesso`;

            //limpar msg
            setTimeout(() => this.msg = "",  3000);

            // limpar campos
            this.nome = "";
            this.shapes = "";
            this.trucks = "";
            this.rodas = "";
            this.rolamentos = "";
            this.opcionais = "";

        }
    },
    mounted() {
        this.getPecas()
    },
    components: {
        Message
    }
}
</script>

<style scoped>
    #skate-form {
        max-width: 400px;
        margin: 0 auto;
    }
    .input-container {
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }
    
    label {
        font-weight: bold;
        margin-bottom: 10px;
        color: #222;
        padding: 0 10px;
        border-left: 4px solid #FCBA03;
    }
    input, select {
        padding: 3px 10px;
        width: 400px;
    }
    #opcionais-container {
        flex-direction: row;
        flex-wrap: wrap;
    }
    .checkbox-container {
        display: flex;
        align-items: flex-start;
        width: 50%;
        margin-bottom: 10px;
        cursor: pointer;
    }
    .checkbox-container span, 
    .checkbox-container input {
        width: auto;
    }  
    .checkbox-container span {
        margin-left: 6px;
        font-weight: bold;
    }
    .paddingEsquerda {
        padding-left: 30px;
    }
    .submit-btn {
        background-color: #222;
        color: #FCBA03;
        font-weight: bold;
        border: 2px solid #222;
        padding: 10px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
    }
    .submit-btn:hover {
        background-color: transparent;
        color: #222;
    }
</style>
