<script setup>
    import { reactive, watch } from 'vue';

    const estado = reactive({
        n1: '',
        n2: '',
        operacao: '+',
        resultado: '',
    })

    const calcularResultado = () => {
        const n1 = parseFloat(estado.n1)
        const n2 = parseFloat(estado.n2)

        if(isNaN(n1) || isNaN(n2)) {
            estado.resultado = "Digite um numero valido ou digite o segundo campo"
            return
        }

        switch(estado.operacao) {
        case "+":  estado.resultado = n1 + n2;
            break;
        case "-":  estado.resultado = n1 - n2;
            break;
        case "*":  estado.resultado = n1 * n2;
            break;
        case "/":  
            estado.resultado = n2 !== 0 ? n1 / n2 : "Erro: divisao por zero";
            break;
        default: estado.resultado = "Operacao invalida"
    }
    }

    watch(() => [estado.n1, estado.n2, estado.operacao], calcularResultado);
</script>
<template>
    <form class="ps-5">
        <div class="row">
            <div class="col-md-3">
                <input v-model="estado.n1" required type="number" placeholder="Numero 1" name="Numero">
            </div>
            <div class="col-md-1">
                <select v-model="estado.operacao" class="form-control p-1">
                    <option value="+">+</option>
                    <option value="-">-</option>
                    <option value="*">x</option>
                    <option value="/">÷</option>
                </select>
            </div>
            <div class="col-md-3">
                <input v-model="estado.n2" required type="number" placeholder="Numero 2" name="Numero">
            </div>
            <div class="col-md-3">
                Resultado: <strong>{{estado.resultado}}</strong>
            </div>
        </div>
    </form>
</template>