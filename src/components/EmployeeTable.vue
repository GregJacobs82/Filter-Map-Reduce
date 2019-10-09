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
                <td>{{ employee.name }}</td>
                <td>{{ employee.email }}</td>
                <td>
                    <button class="round-button btn-sm btn-success">Edit</button>
                    <button @click="$emit('delete:employee', employee.id)" class="round-button btn-sm btn-danger">Delete</button>
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
        }
    }
</script>

<style lang="scss" scoped>
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