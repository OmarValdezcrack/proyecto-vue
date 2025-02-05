<template>
    <div>
        <h2>Formulario de registro</h2>
        <Form :validation-schema="schema" @submit="onSubmit">
            <div class="form">
                <div>
                    <label for="nombre">Nombre:</label>
                    <Field v-model="nombre" type="text" name="nombre" id="nombre" placeholder="Ingrese su nombre"/>
                    <ErrorMessage name="nombre" />
                </div>

                <div class="form">
                    <label for="correo">Correo:</label>
                    <Field v-model="email" type="email" name="email" id="correo" placeholder="Ingrese su email"/>
                    <ErrorMessage name="email" />
                </div>

                <div class="form">
                    <button type="submit">Registrar</button>
                </div>
            </div>
        </Form>
    </div>
</template>

<script setup>
import { Form, Field, ErrorMessage } from 'vee-validate';
import { schema } from '../schemas/validationSchema'; 
import { useRegistrarStore } from '../stores/registrarStore'; 
import { ref } from 'vue';

const registrarStore = useRegistrarStore();
const nombre = ref('');
const email = ref('');

const onSubmit = (values) => {
    registrarStore.guardarRegistro(values.nombre, values.email);
    console.log('Se ha enviado el formulario', values);
};
</script>

<style scoped>
.form {
    margin-bottom: 10px;
}
</style>
