<template>
  <div class="contenedor-formulario">
    <h2>Registrar nuevo usuario</h2>
    <div class="campo-formulario">
      <label>Nombre de Usuario:</label>
      <input type="text" v-model="usuario.nombre">
      <p v-if="errores.nombre" class="error">{{ errores.nombre }}</p>
    </div>

    <div class="campo-formulario">
      <label>Email:</label>
      <input type="email" v-model="usuario.email">
      <p v-if="errores.email" class="error">{{ errores.email }}</p>
    </div>

    <div class="campo-formulario">
      <label>Contraseña:</label>
      <input type="password" v-model="usuario.password">
      <p v-if="errores.password" class="error">{{ errores.password }}</p>
    </div>

    <div class="campo-formulario">
      <label>Fecha de Nacimiento:</label>
      <input type="date" v-model="usuario.fechaNacimiento">
      <p v-if="errores.fechaNacimiento" class="error">{{ errores.fechaNacimiento }}</p>
    </div>

    <button class="boton" @click="registrarUsuario" :disabled="!formularioValido">Registrar</button>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const usuario = ref({
  nombre: '',
  email: '',
  password: '',
  fechaNacimiento: ''
});

const errores = ref({
  nombre: '',
  email: '',
  password: '',
  fechaNacimiento: ''
});

const formularioValido = ref(true);

const validarFormulario = () => {
  errores.value = {}; // Reiniciar errores

  if (!usuario.value.nombre) {
    errores.value.nombre = "El nombre es obligatorio.";
  }

  if (!usuario.value.email) {
    errores.value.email = "El email es obligatorio.";
  } else if (!/\S+@\S+\.\S+/.test(usuario.value.email)) {
    errores.value.email = "El email no es válido.";
  }

  if (!usuario.value.password) {
    errores.value.password = "La contraseña es obligatoria.";
  } else if (usuario.value.password.length < 6) {
    errores.value.password = "La contraseña debe tener al menos 6 caracteres.";
  }

  if (!usuario.value.fechaNacimiento) {
    errores.value.fechaNacimiento = "Debe seleccionar una fecha.";
  }

  // Establecer si el formulario es válido
  formularioValido.value = Object.keys(errores.value).length === 0;
};

const registrarUsuario = () => {
  validarFormulario();

  if (!formularioValido.value) {
    return;
  }

  alert(`Usuario creado correctamente:\nNombre: ${usuario.value.nombre}\nEmail: ${usuario.value.email}`);
  
  usuario.value = { nombre: '', email: '', password: '', fechaNacimiento: '' };
};
</script>

<style>
.contenedor-formulario {
  background: #1c2b3a; /* Fondo oscuro azul */
  color: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
  width: 320px;
  font-family: Arial, sans-serif;
  margin: 0 auto; /* Centra horizontalmente */
  display: flex;
  flex-direction: column;
  align-items: center;
}

.campo-formulario {
  margin-bottom: 15px;
  width: 100%;
}

label {
  display: block;
  font-size: 14px;
  margin-bottom: 5px;
}

input {
  width: calc(100% - 16px);
  padding: 8px;
  border: 1px solid #4a647a; /* Color de borde más oscuro */
  border-radius: 4px;
  font-size: 14px;
  background-color: #2a3d52; /* Fondo de los inputs */
  color: white;
}

.error {
  color: #e74c3c; /* Rojo para los errores */
  font-size: 12px;
  margin-top: 4px;
}

.boton {
  width: 100%;
  padding: 10px;
  background: #007bb5; /* Azul oscuro */
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin-top: 10px;
}

.boton:disabled {
  background: #3a5a7d; /* Azul más claro cuando está deshabilitado */
  cursor: not-allowed;
}

.boton:hover:enabled {
  background: #005f8d; /* Azul más oscuro al pasar el ratón */
}
</style>