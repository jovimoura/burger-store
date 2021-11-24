<template>
    <Message :msg="msg" v-show="msg" />
    <div>
        <form id="burger-form" @submit="createBurger">
            <div class="input-container">
                <label for="nome">Nome do Cliente</label>
                <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite o seu nome">
            </div>
            <div class="input-container">
                <label for="pao">Escolha o pão:</label>
                <select name="pao" v-model="pao" id="pao">
                    <option value="">Selecione o pão</option>
                    <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{pao.tipo}}</option>
                </select>
            </div>
            <div class="input-container">
                <label for="carne">Escolha a carne do seu burger:</label>
                <select v-model="carne" name="carne" id="carne">
                    <option value="">Selecione a carne</option>
                    <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{carne.tipo}}</option>
                </select>
            </div>
            <div class="input-container">
                <label id="opcionais-title" for="opcionais">Selecione os opcionais:</label>
                <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id" >
                    <input type="checkbox" name="opcionais" v-model="opcionais"
                     :value="opcional.tipo">
                    <span>{{opcional.tipo}}</span>
                </div>
            </div>
            <div class="input-container">
                <input type="submit" class="submit-btn" value="Criar meu Burger!"> 
            </div>
        </form>
    </div>
</template>

<script>
import Message from './Message.vue'

export default {
    name:'BurgerForm',
    components: {
        Message
    },
    data() {
        return {
            paes:null,
            carnes: null,
            opcionaisdata:null,
            nome:null,
            pao: null,
            carne:null,
            opcionais: [],
            msg: null
        }
    },
    methods: {
        async getIngredientes() {
            const req = await fetch('http://localhost:3000/ingredientes');
            const data = await req.json();

            this.paes = data.paes;
            this.carnes = data.carnes;
            this.opcionaisdata = data.opcionais;
        },

        async createBurger(e) {

            e.preventDefault();
            
            const data = {
                nome: this.nome,
                pao: this.pao,
                carne: this.carne,
                opcionais: Array.from(this.opcionais),
                status: 'Solicitado'
            }

            const dataJson = JSON.stringify(data)

            const req = await fetch('http://localhost:3000/burgers',{
                method: "POST",
                headers: {"Content-Type": "application/json"},
                body:dataJson

            });

            const res = await req.json();

            //limpar inputs
            this.nome= '';
            this.pao='';
            this.carne='';
            this.opcionais='';
            
            //mensagem
            this.msg = `Pedido N°${res.id} realizado com sucesso!`

            //apagando mensagem
            setTimeout(()=>this.msg='',3000)

        }
    },
    mounted() {
        this.getIngredientes()
    },
}
</script>

<style scoped>
    #burger-form {
        max-width: 10rem;
        margin: 0 auto;
    }

    .input-container {
        display: flex;
        flex-direction: column;
        margin-bottom: 2rem;
    }

    label {
        font-weight: bold;
        margin-bottom: 1.4rem;
        color: #222;
        padding: .4rem .7rem;
        border-left: 4px solid #fcba03;
    }

    input, select {
        padding: .5rem .8rem;
        width: 20rem
    }

    #opcionais-container {
        flex-direction: row;
        flex-wrap: wrap;
    }

    #opcionais-title {
        width: 100%;
    }

    .checkbox-container {
        display: flex;
        align-items: flex-start;
        width: 50%;
        margin-bottom: 1.2rem;
    }

    .checkbox-container span,
    .checkbox-container input {
        width: auto;
    }

    .checkbox-container span {
        font-weight: bold;
        margin-left: .5rem;
    }

    .submit-btn {
        background-color: #222;
        color: #fcba03;
        font-weight: bold;
        border: 2px solid #222;
        padding: .7rem;
        font-size: 1.2rem;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
    }

    .submit-btn:hover {
        background-color: transparent;
        color: #222;
    }

    @media (max-width:768px) {
        #burger-form {
            max-width: 100%;
        }
    }
</style>