<template>
    <section>
        <h3>Añadir Profesores</h3>
        <div>
            <label for="nombre">Nombre</label>
            <input type="text" id="nombre" v-model="teacher.teacherName">
        </div>
        <div>
            <label for="apellido">Apellido</label>
            <input type="text" id="apellido" v-model="teacher.surname">
        </div>
        <div>
            <label for="dni">DNI / CIP</label>
            <input type="text" id="dni" v-model="teacher.dni">
        </div>
        <div>
            <label for="materia">Materias</label>
            <input type="text" id="materia" v-model="subject">
            <button @click="handleSubject">Agregar Materias</button>
        </div>
        <div>
            <ul>
                <li v-for="(element, index) in teacher.subjects" :key="index">{{ element }}</li>
            </ul>
        </div>
        <input type="checkbox" v-model="teacher.doc">Documentacion entregada
        <button @click="handleAddTeacher">Agregar Profesor</button>
    </section>

    <section>
        <h3>Listado de Profesores</h3>
        <table>
            <tr>
                <th>Nombre</th>
                <th>Apellido</th>
                <th>DNI / CIP</th>
                <th>Materias</th>
                <th>Documentacion</th>
            </tr>
            <tr v-for="elemnt in teachers" :key="elemnt.dni">
                <th>{{ elemnt.teacherName }}</th>
                <th>{{ elemnt.surname }}</th>
                <th>{{ elemnt.dni }}</th>
                <th>
                    <li v-for="(item, index) in elemnt.subjects" :key="index">{{ item }}</li>
                </th>
                <th v-if="elemnt.doc">Entregada</th>
                <th v-else>No Entregada</th>
                <button @click="handleDeleteTeacher(elemnt.dni)">Eliminar Profesor</button>
            </tr>
        </table>
    </section>
</template>

<script setup>
    import { ref } from 'vue';

    let teacher = ref({
        teacherName: '',
        surname: '',
        dni:'',
        subjects: [],
        doc: false
    })

    let teachers = ref([])
    let subject = ref('')

    const handleSubject = () => {
        teacher.value.subjects.push(subject.value)
        subject.value = ''
    }

    const handleAddTeacher = () => {
        teachers.value.push({
            teacherName: teacher.value.teacherName,
            surname: teacher.value.surname,
            dni: teacher.value.dni,
            subjects: teacher.value.subjects,
            doc: teacher.value.doc
        })
        teacher.value.teacherName = ''
        teacher.value.surname = ''
        teacher.value.dni = ''
        teacher.value.subjects = []
        teacher.value.doc = false
        subject.value = ''
    }

    const handleDeleteTeacher = (dniTeacher) => {
        teachers.value = teachers.value.filter(teach => teach.dni !== dniTeacher)
    }
</script>

<style scoped>
</style>