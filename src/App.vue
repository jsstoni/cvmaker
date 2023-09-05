<script setup>
import { reactive } from 'vue'
import Title from './components/Title.vue'

const personalized = {
  label: null,
  value: null
}
const experiences = {
  area: null,
  company: null,
  date: null,
  description: null
}
const formations = {
  career: null,
  institute: null,
  date: null
}
const courses = {
  course: null,
  date: null
}
const skills = {
  ability: null
}
const languages = {
  language: null,
  level: null
}
const CvForm = reactive({
  name: null,
  phone: null,
  email: null,
  description: null,
  personalized: [],
  experiences: [],
  formations: [],
  courses: [],
  skills: [],
  languages: []
})
//methods
const addOptions = (option) => {
  CvForm[option].push({ ...[option] })
  Object.keys(CvForm[option]).forEach((index) => {
    if (index < Object.keys(CvForm[option]).length - 1) {
      CvForm[option][index].toggle = false
    } else {
      CvForm[option][index].toggle = true
    }
  })
}
</script>

<template>
  <main>
    <form>
      <div class="d-flex">
        <div class="sidebar">
          <div class="cols">
            <div>
              <label for="">Nombre</label>
              <input type="text" v-model="CvForm.name" />
            </div>
            <div>
              <label for="">Teléfono</label>
              <input type="text" v-model="CvForm.phone" />
            </div>
          </div>
          <label for="">Email</label>
          <input type="text" v-model="CvForm.email" />

          <label for="">Descripción</label>
          <textarea v-model="CvForm.description" rows="2"></textarea>
          <div class="d-flex">
            <div>
              <h3>Experiencias laborales</h3>
              <p>
                Menciona el nombre de la empresa, cargo, fechas de empleo y principales
                contribuciones
              </p>
            </div>
            <div class="ml-auto">
              <button @click.prevent="addOptions('experiences')">Agregar</button>
            </div>
          </div>

          <div v-for="(item, index) in CvForm.experiences" :key="index">
            <Title
              @remove="CvForm.experiences.splice(index, 1)"
              @toggle="item.toggle = !item.toggle"
              :title="`${item.area || 'Area'} - ${item.company || 'Empresa'}`"
            ></Title>
            <div v-if="item.toggle">
              <div class="cols">
                <div>
                  <label for="">Area de empleo</label>
                  <input type="text" v-model="item.area" />
                </div>
                <div>
                  <label for="">Empresa</label>
                  <input type="text" v-model="item.company" />
                </div>
                <div>
                  <label for="">Fecha</label>
                  <input type="text" v-model="item.date" />
                </div>
              </div>
              <label for="">Descripción</label>
              <textarea v-model="item.description" rows="2"></textarea>
            </div>
          </div>

          <div class="d-flex">
            <div>
              <h3>Formaciones académicas</h3>
              <p>
                Enumera tus títulos universitarios, instituciones educativas y fechas de graduación.
              </p>
            </div>
            <div class="ml-auto">
              <button @click.prevent="addOptions('formations')">Agregar</button>
            </div>
          </div>
          <div v-for="(item, index) in CvForm.formations" :key="index">
            <Title
              @remove="CvForm.formations.splice(index, 1)"
              @toggle="item.toggle = !item.toggle"
              :title="`${item.career || 'Profesión'} - ${item.institute || 'Instituto'}`"
            ></Title>
            <div v-if="item.toggle">
              <div class="cols">
                <div>
                  <label for="">Carrera realizada</label>
                  <input type="text" v-model="item.career" />
                </div>
                <div>
                  <label for="">Instituto</label>
                  <input type="text" v-model="item.institute" />
                </div>
                <div>
                  <label for="">Fecha</label>
                  <input type="text" v-model="item.date" />
                </div>
              </div>
            </div>
          </div>

          <div class="d-flex">
            <h3>Cursos realizados</h3>
            <div class="ml-auto">
              <button @click.prevent="addOptions('courses')">Agregar</button>
            </div>
          </div>
          <div v-for="(item, index) in CvForm.courses" :key="index">
            <Title
              @remove="CvForm.courses.splice(index, 1)"
              @toggle="item.toggle = !item.toggle"
              :title="`${item.course || 'Curso'}`"
            ></Title>
            <div v-if="item.toggle">
              <div class="cols">
                <div>
                  <label for="">Curso realizado</label>
                  <input type="text" v-model="item.course" />
                </div>
                <div>
                  <label for="">Fecha</label>
                  <input type="text" v-model="item.date" />
                </div>
              </div>
            </div>
          </div>

          <div class="d-flex">
            <div>
              <h3>Habilidades</h3>
              <p>
                Enumera tus habilidades clave relacionadas con el trabajo, como programación,
                diseño, liderazgo, etc.
              </p>
            </div>
            <div class="ml-auto">
              <button @click.prevent="addOptions('skills')">Agregar</button>
            </div>
          </div>
          <div v-for="(item, index) in CvForm.skills" :key="index">
            <Title
              @remove="CvForm.skills.splice(index, 1)"
              @toggle="item.toggle = !item.toggle"
              :title="`${item.ability || 'Habilidad'}`"
            ></Title>
            <div v-if="item.toggle">
              <label for="">Habilidad</label>
              <input type="text" v-model="item.ability" />
            </div>
          </div>

          <div class="d-flex">
            <div>
              <h3>Idiomas</h3>
              <p>
                Enumera los idiomas que hablas y tu nivel de fluidez en cada uno (por ejemplo,
                básico, medio, avanzado).
              </p>
            </div>
            <div class="ml-auto">
              <button @click.prevent="addOptions('languages')">Agregar</button>
            </div>
          </div>
          <div v-for="(item, index) in CvForm.languages" :key="index">
            <Title
              @remove="CvForm.languages.splice(index, 1)"
              @toggle="item.toggle = !item.toggle"
              :title="`${item.language || 'Idioma'} - ${item.level || 'Nivel'}`"
            ></Title>
            <div v-if="item.toggle">
              <label for="">Idioma</label>
              <input type="text" v-model="item.language" />
              <label for="">Nivel</label>
              <select v-model="item.level">
                <option value="Nivel básico">Nivel básico</option>
                <option value="Nivel medio">Nivel medio</option>
                <option value="Nivel Avanzado">Nivel Avanzado</option>
                <option value="Nativo">Nativo</option>
              </select>
            </div>
          </div>
        </div>
        <div class="content"></div>
      </div>
    </form>
  </main>
</template>
