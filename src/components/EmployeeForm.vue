<template>
    <div id="employee-form">
        <!--
        <form @submit.prevent="handleSubmit">
            <label>Employee name</label>
            <input v-model="employee.name" type="text" />
            <label>Employee Email</label>
            <input v-model="employee.email" type="text" />
            <button>Add Employee</button>
        </form>
        -->
        <form @submit.prevent="handleSubmit">
            <label>Employee name</label>
            <input
                ref="first"
                type="text"
                :class="{ 'has-error': submitting && invalidName }"
                v-model="employee.name"
                @focus="clearStatus"
                @keypress="clearStatus"
            />
            <label>Employee Email</label>
            <input
                type="text"
                :class="{ 'has-error': submitting && invalidEmail }"
                v-model="employee.email"
                @focus="clearStatus"
            />
            <p v-if="error && submitting" class="error-message">
                ❗Please fill out all required fields
            </p>
            <p v-if="success" class="success-message">
                ✅ Employee successfully added
            </p>
            <button>Add Employee</button>
        </form>
    </div>
</template>

<script>
    export default {
        name: 'employee-form',
        data() {
            return {

                // SIMPLE VALIDATION STATES
                submitting: false,
                error: false,
                success: false,

                // LOCAL STATE OF NEW EMPLOYEE
                employee: {
                    name: '',
                    email: '',
                }
            }
        },
        computed: {
            invalidName() {
                return this.employee.name === ''
            },

            invalidEmail() {
                return this.employee.email === ''
            },
        },
        methods: {
            /**
             * SUBMIT w/ SIMPLE VALIDATION
             */
            handleSubmit() {
                // alert('testing handleSubmit');
                this.submitting = true;
                this.clearStatus();

                if (this.invalidName || this.invalidEmail) {
                    this.error = true;
                    return
                }

                this.$emit('add:employee', this.employee);
                this.employee = {
                    name: '',
                    email: '',
                }
                this.error = false;
                this.success = true;
                this.submitting = false;
            },

            /**
             * CLEAR VALIDATION
             */
            clearStatus() {
                this.success = false;
                this.error = false;
            }
        },
    }
</script>

<style scoped>
    form {
        margin-bottom: 2rem;
    }

    [class*='-message'] {
        font-weight: 500;
    }

    .error-message {
        color: #d33c40;
    }

    .success-message {
        color: #32a95d;
    }
</style>