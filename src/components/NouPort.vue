<template>
    <h1>Edita/Crea port</h1>
    <div class="container mt-3">
        <h2>Formulari per Emplenar Elements</h2>
        <form @submit.prevent="afegirElement">
            <div class="form-group">
                <label for="nombre">Nom:</label>
                <input v-model="nouElement.nombre" type="text" class="form-control" id="nombre"
                    placeholder="Introdueix el nom">
            </div>
            <div class="form-group">
                <label for="altura">Altura (metros):</label>
                <input v-model="nouElement.altura_metros" type="number" class="form-control" id="altura"
                    placeholder="Introdueix l'altura">
            </div>
            <div class="form-group">
                <label for="categoria">Categoria:</label>
                <input v-model="nouElement.categoria" type="text" class="form-control" id="categoria"
                    placeholder="Introdueix la categoria">
            </div>
            <div class="form-group">
                <label for="ubicacion">Ubicació:</label>
                <input v-model="nouElement.ubicacion" type="text" class="form-control" id="ubicacion"
                    placeholder="Introdueix la ubicació">
            </div>
            <div class="form-group">
                <label for="etapes">Etapas Destacades:</label>
                <input v-model="etapas" type="text" class="form-control" id="etapes"
                    placeholder="Introdueix les etapes destacades">
            </div>
            <div class="form-group">
                <label for="descripcion">Descripció:</label>
                <textarea v-model="nouElement.descripcion" class="form-control" id="descripcion"
                    placeholder="Introdueix la descripció"></textarea>
            </div>
            <button type="submit" class="btn btn-primary">Afegir Element</button>
            <div class="alert alert-success" role="alert" v-if="portCreatCorrecte">Port creat correctament</div>
        </form>
    </div>
</template>
  
<script>
export default {
    name: 'NouPort',
    data() {
        return {
            etapas: "",
            nouElement: {
                id: 999999,
                nombre: "",
                altura_metros: null,
                categoria: "",
                ubicacion: "",
                etapas_destacadas: [],
                descripcion: ""
            },
            portCreatCorrecte : false,

        };
    },

    props: {
        //msg: String
    },
    methods: {
        afegirElement() {
            // Aquí pots fer el que vulguis amb les dades introduïdes (per exemple, afegir-les a una llista)
            console.log("Element afegit:", this.nouElement);
            this.nouElement.id = Math.floor(Math.random() * 1000000);
            this.nouElement.etapas_destacadas.push(this.etapas);
            this.postPort(this.nouElement);
            this.portCreatCorrecte = true;
            // També pots reiniciar les dades del formulari si és necessari
            this.etapas = "";
            this.nouElement = {
                id: "",
                nombre: "",
                altura_metros: null,
                categoria: "",
                ubicacion: "",
                etapas_destacadas: [],
                descripcion: ""
            };
        },
        async postPort(port) {
            try {
                const response = await fetch('http://localhost:3000/ports', {
                    method: 'POST',
                    body: JSON.stringify(port),
                    headers: { 'Content-type': 'application/json; charset=UTF-8' },
                });

                const portCreado = await response.json();
                console.log(portCreado);
                //this.usuarios = [...this.usuarios, usuarioCreado];
            } catch (error) {
                console.error(error);
            }
        }
    },

    mounted() {

    }

}
</script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>