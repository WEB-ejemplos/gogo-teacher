<template>
    <section>
        <h3>Añadir profesor</h3>
        <div>
            <label>Nombre:</label><input type="text" v-model="teacher.teacherName">
        </div>
        <div>
            <label>Apellidos:</label><input type="text" v-model="teacher.surname">
        </div>
        <div>
            <label>DNI:</label><input type="text" v-model="teacher.dni">
        </div>
        <div>
            <label>Curso:</label><input type="text" v-model="subject">
            <button @click="handleSubjects()">Añadir</button>
        </div>
        <div>
            <ul>
                <li v-for="(elm, index) in teacher.subjects" :key="index">{{ elm }}</li>
            </ul>
        </div>
        <input type="checkbox" v-model="teacher.doc"> Documentación entregada
        <button @click="handleAddTeacher()">Agregar</button>
    </section>
    <section>
        <h3>Listado de Profesores</h3>
        <table>
            <tr>
                <th>Nombre</th>
                <th>Apellidos</th>
                <th>DNI</th>
                <th>Curso</th>
                <th>Documentación Entregada</th>
            </tr>
            <tr v-for="elm in teachers" :key="elm.dni">
                <th>{{elm.teacherName}}</th>
                <th>{{elm.surname}}</th>
                <th>{{elm.dni}}</th>
                <th>
                    <ul>
                        <li v-for="(item, index) in elm.subjects" :key="index">{{ item }}</li>
                    </ul>
                </th>
                <th v-if="elm.doc">Entregado</th>
                <th v-else>No entregado</th>
            </tr>
        </table>
    </section>
</template>

<script lang="ts" setup>
    import {Ref,ref} from 'vue'

    interface ITeacher{
        teacherName: string,
        surname: string,
        dni: string,
        subjects: Array<string>,
        doc: boolean
    }

    let teacher:Ref<ITeacher> = ref({
        teacherName: '',
        surname: '',
        dni: '',
        subjects: [],
        doc: false
    })

    let teachers:Ref<Array<ITeacher>> = ref([])

    let subject:Ref<any> = ref({})

    const handleSubjects = ()=>{
        teacher.value.subjects.push(subject.value)
        subject.value = ''
    }

    const handleAddTeacher = ()=>{
        teachers.value.push(teacher.value)
        teacher.value = {
            teacherName: '',
            surname: '',
            dni: '',
            subjects: [],
            doc: false
        }
    }

</script>

<style scoped></style>