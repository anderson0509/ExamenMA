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

        // Campos obligatorios
        if (!nombre || !edad || !direccion) {
          return alert("Por favor, completa todos los campos.");
        }

        // 🔹 Validar nombre
        if (!/^[A-Za-zÁÉÍÓÚáéíóúÑñ\s]+$/.test(nombre)) {
          return alert("El nombre solo puede contener letras y espacios (sin números ni símbolos).");
        }

        // 🔹 Validar edad
        if (isNaN(edad) || edad < 15 || edad > 80) {
          return alert("La edad debe ser un número válido entre 15 y 80.");
        }

        if (!Number.isInteger(edad)) {
          return alert("La edad debe ser un número entero (sin decimales).");
        }

        // 🔹 Validar dirección
        if (direccion.length < 5) {
          return alert("La dirección debe tener al menos 5 caracteres.");
        }

        if (direccion.length > 100) {
          return alert("La dirección no puede superar los 100 caracteres.");
        }

        if (!/^[a-zA-Z0-9\s#\-\/]+$/.test(direccion)) {
          return alert("La dirección solo puede contener letras, números y los símbolos #, -, /.");
        }

        // Si todo es válido
        alert(
          ` Datos recibidos:\nNombre: ${nombre}\nEdad: ${edad}\nDirección: ${direccion}`
        );

        this.limpiarFormulario();
      } catch (error) {
        console.error("Error al validar el formulario:", error);
        alert("Ocurrió un error al validar el formulario.");
      }
    },

    limpiarFormulario() {
      this.nombre = "";
      this.edad = "";
      this.direccion = "";
    },
  },
};
</script>

<style scoped>
.form {
  max-width: 400px;
  margin: 40px auto;
  padding: 20px;
  background-color: #ffffff;
  border: 1px solid #ddd;
  border-radius: 10px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}
.form label {
  display: block;
  margin-bottom: 6px;
  font-weight: bold;
  color: #555;
}
.form input {
  width: 100%;
  padding: 10px;
  margin-bottom: 15px;
  border: 1px solid #ccc;
  border-radius: 6px;
  font-size: 14px;
  box-sizing: border-box;
  transition: border-color 0.3s;
}
.form button {
  width: 100%;
  padding: 10px;
  background-color: #00897b;
  color: #fff;
  border: none;
  border-radius: 6px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s;
}
.form button:hover {
  background-color: #00796b;
}
</style>
