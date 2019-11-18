<template>
    <div class="user-form">
        <form class="mb-4" v-on:submit.prevent="submitUser">
            <div class="form-group">
                <label for="name">Name</label>
                <input 
                    ref="first"
                    type="text" 
                    :class="{ 'has-error': submitting && invalidName }"
                    class="form-control" 
                    v-model="user.name"
                    @focus="clearStatus"
                    @keypress="clearStatus"
                />
            </div>
            <div class="form-group">
                <label for="email">Email</label>
                <input 
                    type="email" 
                    :class="{ 'has-error': submitting && invalidEmail }"
                    class="form-control" 
                    v-model="user.email"
                    @focus="clearStatus"
                    @keypress="clearStatus"
                />
            </div>
            <div v-if="error && submitting" class="alert alert-danger">
                Please fill out all required fields
            </div>
            <div v-if="success" class="alert alert-success">
                User successfully added
            </div>
            <button class="btn btn-primary">Add User</button>
        </form>
    </div>
</template>

<script>
    export default {
        name: 'UserForm',
        data() {
            return {
                submitting: false,
                error: false,
                success: false,
                user: {
                    name: '',
                    email: ''
                },
            }
        },
        methods: {
            submitUser() {
                this.submitting = true;
                this.clearStatus();

                if(this.invalidName || this.invalidEmail) {
                    this.error = true
                    return
                }

                this.$emit('add:user', this.user);
                this.user = {
                    name: '',
                    email: ''
                }

                this.error = false
                this.success = true
                this.submitting = false
            },

            clearStatus() {
                this.error = false
                this.success = false
            }
        },
        computed: {
            invalidName() {
                return this.user.name === '';
            },

            invalidEmail() {
                return this.user.email === '';
            }
        }
    }
</script>

<style>

</style>