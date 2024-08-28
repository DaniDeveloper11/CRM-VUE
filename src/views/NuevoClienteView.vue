<script setup>
import ClienteService from '@/services/ClienteService';
import { useRouter } from 'vue-router';
import { FormKit } from '@formkit/vue'
import RouterLink from '../components/UI/RouterLink.vue'
import Header from '../components/UI/Heading.vue'
import router from '@/router';

defineProps({
    titulo: {
        type: String
    }
})


const handleSubmit = (data) => {
    data.estado = 1;
    ClienteService.agregarCliente(data)
        .then(respuesta => console.log(respuesta))
        router.push({name:'home'})
        .catch(error => console.log(error))
}

</script>


<template>
    <div>
        <div class="flex justify-end">
            <RouterLink to="home">
                Volver
            </RouterLink>
        </div>
        <Header>{{ titulo }}</Header>

        <div class="mx-auto mt-10 bg-white shadow">
            <div class="mx-auto md:w-2/3 py-20 px-6 ">
                <FormKit @submit="handleSubmit"
                    type="form" submit-label="Agregar Cliente" incomplete-message="No se pudo enviar, Revisa los mensajes">
                    
                    <FormKit type="text" name="nombre" label="Nombre" placeholder="Nombre del Cliente"
                        help="Coloca el nombre del Cliente que deseas registrar" validation="required"
                        :validation-messages="{ required: 'El nombre del cliente es Obligatorio' }"
                        validation-visibility="submit"></FormKit>

                        <FormKit type="text" name="apellido" label="Apellido" placeholder="Apellido del Cliente"
                        help="Coloca el apellido del Cliente que deseas registrar" validation="required"
                        :validation-messages="{ required: 'El apellido del cliente es Obligatorio' }"
                        validation-visibility="submit"></FormKit>

                        
                        <FormKit type="email" name="email" label="Email" placeholder="Email del Cliente"
                        help="Coloca el email del Cliente que deseas registrar" validation="required | email"
                        :validation-messages="{ required: 'El email es obligatorio', email:'Coloca un email Valido' }"
                        validation-visibility="submit"></FormKit>

                        <FormKit type="text" name="telefono" label="Telefono" placeholder="Telefono: XXX-XXX-XXXX"
                        help="Coloca el telefono del Cliente que deseas registrar" validation="required|*matches:/^[0-9]{3}-[0-9]{3}-[0-9]{4}$/"
                        :validation-messages="{ matches:'El Formato no es valido'}"></FormKit>

                        <FormKit type="text" name="empresa" label="Empresa" placeholder="Empresa del cliente"
                        ></FormKit>

                        <FormKit type="text" name="puesto" label="Puesto" placeholder="Puesto del cliente"
                        ></FormKit>

                </FormKit>
            </div>

        </div>

    </div>
</template>
<style>
.formkit-wrapper{
    max-width: 100%;
}
</style>
