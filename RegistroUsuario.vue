<template>
  <div class="max-w-md mx-auto mt-10 p-6 bg-white rounded-2xl shadow-lg">
    <h2 class="text-2xl font-bold text-center mb-4">Registro de Usuario</h2>

    <form @submit.prevent="validarFormulario">
      <!-- Campo Nombre -->
      <div class="mb-4">
        <label class="block font-semibold mb-1">Nombre:</label>
        <input
          v-model="nombre"
          type="text"
          placeholder="Ej. Juan Pérez"
          class="w-full border rounded-lg p-2"
        />
        <p v-if="errores.nombre" class="text-red-500 text-sm mt-1">
          {{ errores.nombre }}
        </p>
      </div>

      <!-- Campo Dirección -->
      <div class="mb-4">
        <label class="block font-semibold mb-1">Dirección:</label>
        <input
          v-model="direccion"
          type="text"
          placeholder="Ej. Col. Escalón #45"
          class="w-full border rounded-lg p-2"
        />
        <p v-if="errores.direccion" class="text-red-500 text-sm mt-1">
          {{ errores.direccion }}
        </p>
      </div>

      <!-- Campo Edad -->
      <div class="mb-4">
        <label class="block font-semibold mb-1">Edad:</label>
        <input
          v-model="edad"
          type="number"
          placeholder="Ej. 25"
          class="w-full border rounded-lg p-2"
        />
        <p v-if="errores.edad" class="text-red-500 text-sm mt-1">
          {{ errores.edad }}
        </p>
      </div>

      <!-- Botón de envío -->
      <button
        type="submit"
        class="w-full bg-blue-600 text-white font-semibold py-2 rounded-lg hover:bg-blue-700 transition"
      >
        Registrar
      </button>
    </form>

    <!-- Mensaje de éxito -->
    <div v-if="exito" class="mt-4 text-green-600 font-semibold text-center">
      ✅ Registro exitoso.
    </div>
  </div>
</template>

<script>
export default {
  name: "RegistroUsuario",
  data() {
    return {
      nombre: "",
      direccion: "",
      edad: "",
      errores: {},
      exito: false,
    };
  },
  methods: {
    validarFormulario() {
      this.errores = {};
      this.exito = false;

      // Validar Nombre
      if (!this.nombre) {
        this.errores.nombre = "El nombre es obligatorio.";
      } else if (this.nombre.length < 3) {
        this.errores.nombre = "El nombre debe tener al menos 3 caracteres.";
      } else if (!/^[a-zA-ZÁÉÍÓÚáéíóúñÑ\s]+$/.test(this.nombre)) {
        this.errores.nombre = "El nombre solo debe contener letras.";
      }

      // Validar Dirección
      if (!this.direccion) {
        this.errores.direccion = "La dirección es obligatoria.";
      } else if (this.direccion.length < 5) {
        this.errores.direccion =
          "La dirección debe tener al menos 5 caracteres.";
      }

      // Validar Edad
      if (!this.edad) {
        this.errores.edad = "La edad es obligatoria.";
      } else if (isNaN(this.edad)) {
        this.errores.edad = "La edad debe ser numérica.";
      } else if (this.edad < 18) {
        this.errores.edad = "Debe tener al menos 18 años.";
      } else if (this.edad > 100) {
        this.errores.edad = "La edad no puede ser mayor de 100.";
      }

      // Si no hay errores
      if (Object.keys(this.errores).length === 0) {
        this.exito = true;
        console.log("Registro correcto:", {
          nombre: this.nombre,
          direccion: this.direccion,
          edad: this.edad,
        });
      }
    },
  },
};
</script>

<style scoped>
body {
  background-color: red;
}
</style>
