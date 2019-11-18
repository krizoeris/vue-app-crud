<template>
    <div class="user-table">
        <div v-if="users.length < 1" class="alert alert-light">
            No Users
        </div>
        <table v-else class="table table-bordered">
            <thead>
                <tr>
                    <th>Name</th>
                    <th>Email</th>
                    <th></th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="user in users" :key="user.id">
                    <td v-if="editing === user.id">
                        <input type="text" v-model="user.name">
                    </td>
                    <td v-else>{{ user.name }}</td>
                    <td v-if="editing === user.id">
                        <input type="email" v-model="user.email">
                    </td>
                    <td v-else>{{ user.email }}</td>
                    <td v-if="editing === user.id">
                        <button @click="editUser(user)" class="btn btn-primary mr-1">Save</button>
                        <button @click="cancelEdit(user)" class="btn btn-light">Cancel</button>
                    </td>
                    <td v-else>
                        <button @click="editMode(user)" class="btn btn-warning mr-1">Edit</button>
                        <button @click="$emit('delete:user', user.id)" class="btn btn-danger">Delete</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
    export default {
        name: 'UsersTable',
        props: {
            users: Array
        },
        data() {
            return {
                editing: null,
                cachedUser: null
            }
        },
        methods: {
            editMode(user) {
                this.cachedUser = Object.assign({}, user)
                this.editing = user.id
            },

            cancelEdit(user) {
                Object.assign(user, this.cachedUser)
                this.editing = null
            },

            editUser(user) {
                if(user.name === '' || user.email === '') return
                this.$emit('edit:user', user.id, user)
                this.editing = null
            }
        }
    }
</script>

<style></style>