<template>
    <div id="employee-table">
        <table>
            <thead>
            <tr>
                <th>Employee name</th>
                <th>Employee email</th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="(employee, id) in employees" :key="id">
                <td>{{ employee.name }}</td>
                <td>{{ employee.email }}</td>
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

<style scoped></style>