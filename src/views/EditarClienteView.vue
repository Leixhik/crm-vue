<script setup>
import { onMounted } from "vue";
import { FormKit } from "@formkit/vue";
import { useRouter, useRoute } from "vue-router";
import ClienteService from "../services/ClienteService";
import RouterLink from "@/components/UI/RouterLink.vue";
import Heading from "@/components/UI/Heading.vue";

const router = useRouter()
const route = useRoute()

const { id } = route.params

onMounted(() => {
  ClienteService.obtenerCliente(id)
  .then(({data}) => console.log(data))
  .catch(error => console.log(error))
})

defineProps({
  titulo: {
    type: String,
  },
});

  const handleSubmit = (data) => {

  }
</script>

<template>
  <div>
    <!-- Todo el campo del form para agregar cliente  -->
    <div class="flex justify-end">
      <RouterLink to="listado-clientes"> Volver </RouterLink>
    </div>
    <Heading>{{ titulo }}</Heading>

    <div class="mx-auto mt-10 bg-white shadow">
      <div class="mx-auto md:w-2/3 py-20 px-6">
        <FormKit
          type="form"
          submit-label="Agregar Cliente"
          incomplete-message="No se pudo enviar, revisa los mensajes"
          @submit="handleSubmit"
        >
          <FormKit
            type="text"
            label="Nombre"
            name="nombre"
            placeholder="Nombre de Cliente"
            validation="required"
            :validation-messages="{ required: 'El nombre del cliente es obligatorio' }"
          />

          <FormKit
            type="text"
            label="Apellido"
            name="apellido"
            placeholder="Apellido de Cliente"
            validation="required"
            :validation-messages="{ required: 'El apellido del cliente es obligatorio' }"
          />

          <FormKit
            type="text"
            label="Email"
            name="email"
            placeholder="Email de Cliente"
            validation="required|email"
            :validation-messages="{
              required: 'El email del cliente es obligatorio',
              email: 'Coloca un email válido',
            }"
          />

          <FormKit
            type="text"
            label="Télefono"
            name="telefono"
            placeholder="Teléfono: XXX-XXX-XXXX"
            validation="*matches:/^[0-9]{3}-[0-9]{3}-[0-9]{4}$/"
            :validation-messages="{
              matches: 'El Formato no es válido'
            }"
          />

          <FormKit
            type="text"
            name="empresa"
            label="Empresa"
            placeholder="Empresa de Cliente"
          />

          <FormKit
            type="text"
            name="puesto"
            label="Puesto"
            placeholder="Puesto de Cliente"
          />
        </FormKit>
      </div>
    </div>
  </div>
</template>

<style>
.formkit-outer {
  max-width: 100%;
}
</style>


<!-- Usuario llena formulario
      FormKit valida los campos
      Si es válido -> @submit="handleSubmit"
      axios.post() envía datos a JSON Server
      JSON Server guarda en db.json
      Redirección a la lista de clientes
-->