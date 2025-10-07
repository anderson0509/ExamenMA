<template>
  <div>
    <h1>Formulario de prueba</h1>
    <div class="form">
      <form @submit.prevent="validarFormulario">
        <label>Nombre:</label>
        <input type="text" v-model="nombre" />

        <label>Edad:</label>
        <input type="number" v-model="edad" />

        <label>Dirección:</label>
        <input type="text" v-model="direccion" />

        <button type="submit">Enviar</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "FormularioUser",

  data() {
    return {
      nombre: "",
      edad: "",
      direccion: "",
    };
  },

  methods: {
    validarFormulario() {
      try {
        const nombre = this.nombre.trim();
        const edad = Number(this.edad);
        const direccion = this.direccion.trim();

        // Validaciones
        if (!nombre || !edad || !direccion) {
          return alert("Por favor, completa todos los campos.");
        }

        if (isNaN(edad) || edad < 15 || edad > 80) {
          return alert("La edad debe ser un número válido entre 15 y 80.");
        }

        if (!/^[a-zA-Z\s]+$/.test(nombre)) {
          return alert("El nombre solo puede contener letras y espacios.");
        }

        if (direccion.length < 5) {
          return alert("La dirección debe tener al menos 5 caracteres.");
        }

        // Si todo es válido
        alert(
          ` Datos recibidos:\nNombre: ${nombre}\nEdad: ${edad}\nDirección: ${direccion}`
        );

        // 🧹 Limpiar los campos del formulario
        this.limpiarFormulario();
      } catch (error) {
        console.error("Error al validar el formulario:", error);
        alert("Ocurrió un error al validar el formulario.");
      }
    },

    // Nuevo método para limpiar campos
    limpiarFormulario() {
      this.nombre = "";
      this.edad = "";
      this.direccion = "";
    },
  },
};
</script>