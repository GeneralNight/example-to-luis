<template>
    <div>
        <nuxt-link :to="`/profile/${this.$route.params.id}/edit`">Profile</nuxt-link>
        <div class="d-flex flex-column" v-if="showList">
            <div class="todo mb-3" v-for="(todo,index) in todolist" :key="index">
                <input type="checkbox" name="" id="" v-model="todo.done">
                <input type="text" v-model="todo.atividade">
        <button class="btn btn-primary" @click="removeTask(index)">
            Remover
        </button>
    </div>
    <button class="btn btn-primary" @click="addTask">
        Adicionar
    </button>

    <form @submit.prevent="sendForm()" class="d-flex flex-column">
        <input :class="{'input-error':formError.name}" type="text" v-model="form.name"/>
        <input type="text" v-model="form.phone"/>
        <input type="text" v-model="form.email"/>
        <button type="submit" class="btn btn-primary">
            Adicionar
        </button>
    </form>
    
</div>
<p v-else>Carregando...</p>
</div>
</template>

<script>
import {api} from '~/services'
export default {
name: "Todo",
data() {
    return {
        profile: null,
        showList: false, 
        todolist: [
            
        ],
        form: {
            name: "",
            phone: "",
            email: ""
        },
        formError: {
            name: true,
            phone: true,
            email: true
        }
    }
},
methods: {
    addTask() {
        let newTask = {
            atividade: "",
            done: false
        }

        this.todolist.push(newTask)
    },
    removeTask(index) {
        this.todolist.splice(index,1)
    },
    sendForm() {
        console.log(this.form)
    },
    async getProfile() {
        let profileId = this.$route.params.id ?? ''
        await api.getProfile(profileId).then(res=> {
            console.log(res.data)
        }).catch(err=> {
            console.log(err.data)
        })
    }
},
mounted() {
    this.getProfile()
    setTimeout(() => {
        this.showList = true

        setTimeout(() => {
            this.profile = {
                name: "Gui",
                email: "test@gmail.com"
            }
        }, 3000);

    }, 5000);
},
computed: {
    checkProfile() {
        if(this.profile) {
            return true
        }
        return false
    }
},
watch: {
    showList() {
        alert('Carregou Lista')
    },
    checkProfile() {
        // if(this.checkProfile) {
            alert('Carregou Perfil')
        // }
    }
}
}
</script>

<style>
.input-error {
    border-color: red;
}
</style>