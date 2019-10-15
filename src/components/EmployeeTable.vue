<template>
    <div id="employee-table">
        <p v-if="employees.length < 1" class="empty-table">
            No employees
        </p>
        <table v-else>
            <thead>
            <tr>
                <th>Employee name</th>
                <th>Employee email</th>
                <th>Actions</th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="employee in employees" :key="employee.id">
                <td>
                    <input v-if="editing === employee.id" type="text" v-model="employee.name" />
                    <span v-else>{{ employee.name }}</span>
                </td>
                <td>
                    <input v-if="editing === employee.id" type="text" v-model="employee.email" />
                    <span v-else>{{ employee.email }}</span>
                </td>
                <td>
                    <div v-if="editing === employee.id">
                        <button @click="editEmployee(employee)" class="btn-sm btn-success">Save</button>
                        <button @click="cancelEdit(employee)" class="btn-sm btn-danger">Cancel</button>
                    </div>
                    <div v-else>
                        <button @click="editMode(employee)" class="round-button btn-sm btn-success">Edit</button>
                        <button @click="$emit('delete:employee', employee.id)" class="round-button btn-sm btn-danger">Delete</button>
                    </div>
                </td>
            </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
    export default {
        name: 'employee-table',
        props: {
            employees: {
                type: Array,
                default: null,
            }
        },
        data () {
            return {
                editing: null,
                cachedEmployee: null,
            }
        },
        methods: {
            /**
             * EDIT MODE
             * An editing state that will get set to the id of the row that's currently
             * being edited when editMode is enabled.
             * @param employee
             */
            editMode(employee) {
                this.cachedEmployee = Object.assign({}, employee);
                this.editing = employee.id;
            },

            /**
             * CANCEL EDIT MODE
             * Make a cached employee that we can return to.
             * @param employee
             */
            cancelEdit(employee) {
                Object.assign(employee, this.cachedEmployee);
                this.editing = null;
            },

            /**
             * EDIT EMPLOYEE
             * Emits edit:employee to App if the fields aren't empty, and resets the editing state.
             * @param employee
             */
            editEmployee(employee) {
                if (employee.name === '' || employee.email === '') return;
                this.$emit('edit:employee', employee.id, employee);
                this.editing = null;
            }
        }
    }
</script>

<style lang="scss" scoped>

    //*** PAGE ***/
    #employee-table {
        margin-bottom: 180px;
    }

    //*** BUTTONS ***/
    $color-default: rgba(0,0,0,.5);
    $color-success: rgba(15,175,15,1);
    $color-danger: rgba(175,5,5,1);

    .btn-sm {
        font-size: .85rem;
        padding: .375rem .625rem;// .75rem 1.25rem
        transition: all 300ms ease-in-out;
        &:hover,
        &:active,
        &:focus {
            background: $color-default;
            border-color: $color-default;
            transition: all 150ms ease-in-out;
            outline: none;
        }
    }
    .btn-success {
        background: $color-success;
        border-color: $color-success;
        margin-right: 5px;
    }
    .btn-danger {
        background: $color-danger;
        border-color: $color-danger;
    }
</style>