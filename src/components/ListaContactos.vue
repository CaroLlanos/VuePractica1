//Parte del html
<template>
  <div>
    <h1>Practica 1 Vue</h1>
    <br>
    <h2> Lista de Contactos</h2>
    <br>
    <label>
      Filtro:
      <input v-model="filtro" placeholder="Filtrar">
    </label>
    <br>
    <br>
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>Nombre</th>
          <th>Correo Electronico</th>
          <th>Direccion</th>
          <th>Telefono</th>
          <th>Pais</th>
          <th>Ciudad</th>
          <th>Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td><button @click="agregarContacto">Agregar</button></td>
          <td><input v-model="nuevoContacto.nombre" placeholder="Nombre"></td>
          <td><input v-model="nuevoContacto.email" placeholder="Correo Electronico"></td>
          <td><input v-model="nuevoContacto.direccion" placeholder="Direccion"></td>
          <td><input v-model="nuevoContacto.telefono" placeholder="Telefono"></td>
          <td><input v-model="nuevoContacto.pais" placeholder="Pais"></td>
          <td><input v-model="nuevoContacto.ciudad" placeholder="Ciudad"></td>
          <td><button @click="guardarContacto">Guardar</button></td>
        </tr>
        <tr v-for="(contacto) in contactosFiltrados" :key="contacto.id">
          <td>{{ contacto.id }}</td>
          <td>{{ contacto.nombre }}</td>
          <td>{{ contacto.email }}</td>
          <td>{{ contacto.direccion }}</td>
          <td>{{ contacto.telefono }}</td>
          <td>{{ contacto.pais }}</td>
          <td>{{ contacto.ciudad }}</td>
          <td>
            <button @click="editarContacto(contacto)">Editar</button>
            <button @click="eliminarContacto(contacto.id)">Eliminar</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

//Parte de la logica
<script>
export default {
  data() {
    return {
      contactos: [
        {
          id: 1,
          nombre: 'Alice Johnson',
          email: 'alice.johnson@example.com',
          direccion: '123 Maple Street',
          telefono: '123-456-7890',
          pais: 'USA',
          ciudad: 'New York'
        },
        {
          id: 2,
          nombre: 'Bob Smith',
          email: 'bob.smith@example.com',
          direccion: '456 Oak Avenue',
          telefono: '987-654-3210',
          pais: 'Canada',
          ciudad: 'Toronto'
        },
        {
          id: 3,
          nombre: 'Carol White',
          email: 'carol.white@wxample.com',
          direccion: '789 Pine Road',
          telefono: '555-123-4567',
          pais: 'UK',
          ciudad: 'London'
        },
        {
          id: 4,
          nombre: 'David Brown',
          email: 'david.brown@example.com',
          direccion: '321 Elm Street',
          telefono: '444-555-6666',
          pais: 'Australia',
          ciudad: 'Sidney'
        },
        {
          id: 5,
          nombre: 'Emily Davis',
          email: 'emily.davis@example.com',
          direccion: '654 Spruce Lane',
          telefono: '333-444-5555',
          pais: 'USA',
          ciudad: 'Los Angeles'
        }
        
      ],
      nuevoContacto: { id: null, nombre: '', email: '', direccion: '', telefono: '', pais: '', ciudad: '' },
      filtro: '',
      modoEdicion: false,
    };
  },
  computed: {
    contactosFiltrados() {
      return this.contactos.filter(contacto => 
        contacto.nombre.toLowerCase().includes(this.filtro.toLowerCase()) ||
        contacto.email.toLowerCase().includes(this.filtro.toLowerCase())
      );
    }
  },
  methods: {
    agregarContacto() {
      this.nuevoContacto = { id: null, nombre: '', email: '', direccion: '', telefono: '', pais: '', ciudad: '' };
      this.modoEdicion = false;
    },
    guardarContacto() {
      if (this.modoEdicion) {
        const index = this.contactos.findIndex(c => c.id === this.nuevoContacto.id);
        this.contactos.splice(index, 1, { ...this.nuevoContacto });
      } else {
        this.nuevoContacto.id = Date.now();
        this.contactos.push({ ...this.nuevoContacto });
      }
      this.nuevoContacto = { id: null, nombre: '', email: '', direccion: '', telefono: '', pais: '', ciudad: '' };
      this.modoEdicion = false;
    },
    editarContacto(contacto) {
      this.nuevoContacto = { ...contacto };
      this.modoEdicion = true;
    },
    eliminarContacto(id) {
      this.contactos = this.contactos.filter(contacto => contacto.id !== id);
    }
  }
};
</script>


//Estilos
<style scoped>
table {
  width: 100%;
  border-collapse: collapse;
}
th, td {
  border: 1px solid #ccc;
  padding: 10px;
  text-align: left;
}
th {
  background-color: #f4f4f4;
}
button {
  margin: 0 5px;
}
</style>
