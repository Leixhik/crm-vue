<script setup>
import axios from "axios";
import { FormKit } from "@formkit/vue";
import { useRouter } from "vue-router";
import RouterLink from "@/components/UI/RouterLink.vue";
import Heading from "@/components/UI/Heading.vue";

const router = useRouter()

defineProps({
  titulo: {
    type: String,
  },
});

  const handleSubmit = (data) => {
    axios.post("http://localhost:4000/clientes", data)
    .then(respuesta => {
      console.log(respuesta)
      // Redireccionar
      router.push({ name: 'inicio'})
    })
    .catch(error => console.log(error))
  }
</script>

<template>
  <div>
    <div class="flex justify-end">
      <RouterLink to="inicio"> Volver </RouterLink>
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
