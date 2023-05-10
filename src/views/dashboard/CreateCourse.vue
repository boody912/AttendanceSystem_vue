<template>
    <div  v-if= "this.$store.state.user.isAuthenticated && (userGroup === 'ADMIN'|| userGroup === 'TEACHER')">
    <div class="about">
        <div class="hero is-info">
            <div class="hero-body notehome has-text-centered">
                <h1 class="title">Create course</h1>
            </div>
        </div>

        <section class="section">
            <div class="mb-6 px-6 py-4 has-background-grey-lighter">
                <h2 class="subtitle">Meta information</h2>

                <div class="field">
                    <label>Title</label>
                    <input type="text" class="input" v-model="form.title">
                </div>

                <div class="field">
                    <label>Short description</label>
                    <textarea class="textarea" v-model="form.short_description"></textarea>
                </div>

                <div class="field">
                    <label>Long description</label>
                    <textarea class="textarea" v-model="form.long_description"></textarea>
                </div>

                <div class="field">
                    <label>Image:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</label>
                    <input type="file" @change="handleFileUpload">
                </div>
            
                <div class="field">
                    <div class="select is-multiple">
                        <select multiple size="3" v-model="form.categories">
                            <option 
                                v-for="category in categories"
                                v-bind:key="category.id"
                                v-bind:value="category.id"
                            >
                                {{ category.title }}
                            </option>
                        </select>
                    </div>
                </div>
            </div>

            <div class="mb-6 px-6 py-4 has-background-grey-lighter">
                <h2 class="subtitle">Lessons</h2>

                <div
                    v-for="(lesson, index) in form.lessons"
                    v-bind:key="index"
                    class="mb-4"
                >
                    <h3 class="subtitle is-size-6">Lesson</h3>

                    <div class="field">
                        <label>Title</label>
                        <input 
                            type="text" 
                            class="input" 
                            v-model="lesson.title"
                            :name="`form.lessons[${index}][title]`"
                        >
                    </div>

                    <div class="field">
                        <label>Short description</label>
                        <textarea class="textarea" v-model="lesson.short_description" :name="`form.lessons[${index}][short_description]`"></textarea>
                    </div>

                    <div class="field">
                        <label>Long description</label>
                        <textarea class="textarea" v-model="lesson.long_description" :name="`form.lessons[${index}][long_description]`"></textarea>
                    </div>

                    <div class="field">
                        <label>Lesson Type:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</label>
                        <div class="select">
                            <select v-model="lesson.lesson_type" :name="`form.lessons[${index}][lesson_type]`">
                            <option value="VIDEO">Video</option>
                            <option value="ARTICLE">Article</option>
                            </select>
                        </div>
                    </div>


                    <div class="field">
                        <label>Youtube id</label>
                        <input 
                            type="text" 
                            class="input" 
                            v-model="lesson.youtube_id"
                            :name="`form.lessons[${index}][youtube_id]`"
                        >
                    </div>

                    <hr>
                </div>

                <button class="button is-primary" @click="addLesson()">Add lesson</button>
            </div>

            <div class="field buttons">
                <router-link to="/courses" @click="submitForm('draft')" class="button is-success">save as draft</router-link>
                <router-link to="/courses" @click="submitForm('in_review')" class="button is-info">submit for review</router-link>
            </div>
        </section>
    </div>
    </div>
    <div v-else>
         <h2 style="margin-left: 40%;">{{ userGroup }} Can't Access this Page </h2>

    </div>

</template>

<script>
import axios from 'axios'

export default {
    data() {
        return {
            form: {
                title: '',
                short_description: '',
                long_description: '',
                /* youtube_id: '',
                lesson_type: '', */
                categories: [],
                status: '',
                image: null,
                lessons: []
            },

            userGroup: null,
            categories: [],
            types: ['ARTICLE','VIDEO'],
        }
    },
    mounted() {
        axios.get('courses/user_group/')
        .then(response => {
        this.userGroup = response.data.group;
        })
        .catch(error => {
        console.log(error);
        });
        this.getCategories()
    },
    methods: {
        getCategories() {
            console.log('getCategories')

            axios
                .get('courses/get_categories/')
                .then(response => {
                    console.log(response.data)

                    this.categories = response.data
                })
        },
        handleFileUpload(event) {
            this.form.image = event.target.files[0];
        },
        submitForm(status) {
            console.log('submitForm')
            console.log(this.form)

            const formData = new FormData();
            formData.append('title', this.form.title);
            formData.append('short_description', this.form.short_description);
            formData.append('long_description', this.form.long_description);
            formData.append('image', this.form.image);
            formData.append('status', this.form.status);
            formData.append('categories', this.form.categories );
            this.form.status = status
            


            axios
                .post('courses/create/', formData)
                .then(response => {
                    console.log(response.data)
                })
                .catch(error => {
                    console.log('error:', error)
                })
        },
        addLesson() {
            console.log('addLesson')

            this.form.lessons.push({
                title: '',
                short_description: '',
                long_description: '',
                youtube_id:'',
                lesson_type:'',
            })
        }
    }
}
</script>

<style>
  .notehome {
      text-align: center;
   
      height: 80px;
      background: -webkit-linear-gradient(left, #24a0ed, #607d8b);
      color: #fff;
      font-weight: bold;
      line-height: 80px;
    }

</style>