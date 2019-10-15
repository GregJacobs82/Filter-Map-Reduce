<template>
    <div class="home">
        <!--
        <img alt="Vue logo" src="../assets/logo.png">
        <HelloWorld msg="Welcome to Your Vue.js App"/>
        -->
        <div class="small-container">
            <h1>Employees <span class="badge">{{ employees.length }}</span></h1>
            <EmployeeForm @add:employee="addEmployee"/>
            <EmployeeTable
                :employees="employees"
                @edit:employee="editEmployee"
                @delete:employee="deleteEmployee"
            />
        </div>
    </div>
</template>

<script>
    // @ is an alias to /src
    import HelloWorld from '@/components/HelloWorld.vue'
    import EmployeeTable from '@/components/EmployeeTable.vue'
    import EmployeeForm from "@/components/EmployeeForm";


    export default {
        name: 'home',

        components: {
            EmployeeForm,
            HelloWorld,
            EmployeeTable
        },

        data() {
            return {

                // USE API DATA FROM JSONPLACEHOLDER
                employees: [],

                //todo: remove this after we get JSON API data working
                employeesExample: [
                    {
                        id: 1,
                        name: 'Jimi Hendrix',
                        email: 'jimihendrix@example.com',
                    },
                    {
                        id: 2,
                        name: 'Oscar Wilde',
                        email: 'oscar@example.com',
                    },
                    {
                        id: 3,
                        name: 'Bill Murray',
                        email: 'billmurray@example.com',
                    },
                    {
                        id: 4,
                        name: 'Josh Miller',
                        email: 'joshmiller@example.com',
                    },
                ],
            }
        },

        mounted() {
            this.getEmployees();
        },

        methods: {

            /**
             * API GET
             */
            async getEmployees() {
                try {
                    const response = await fetch('https://jsonplaceholder.typicode.com/users');
                    const data = await response.json();
                    this.employees = data;
                } catch (error) {
                    console.error(error);
                }
            },
            /**
             * API POST
             *
             * CREATE A NEW EMPLOYEE
             * @param employee             *
             */
            async addEmployee(employee) {
                try {
                    const response = await fetch('https://jsonplaceholder.typicode.com/users', {
                        method: 'POST',
                        body: JSON.stringify(employee),
                        headers: { "Content-type": "application/json; charset=UTF-8" }
                    });

                    /* NEED TO ADD THE ID
                    const lastId =
                        this.employees.length > 0
                            ? this.employees[this.employees.length - 1].id
                            : 0;
                    const id = lastId + 1;
                    */

                    const data = await response.json();
                    this.employees = [...this.employees, data];
                } catch (error) {
                    console.error(error);
                }
            },
            /**
             * API PUT
             *
             * EDIT EMPLOYEE
             * Take id and updatedEmployee parameters, map through the employees array, and update the correct employee.
             * @param id, updatedEmployee
             */
            async editEmployee(id, updatedEmployee) {
                try {
                    const response = await fetch(`https://jsonplaceholder.typicode.com/users/${id}`, {
                        method: 'PUT',
                        body: JSON.stringify(updatedEmployee),
                        headers: { "Content-type": "application/json; charset=UTF-8" }
                    });
                    const data = await response.json();
                    this.employees = this.employees.map(employee => employee.id === id ? data : employee);
                } catch (error) {
                    console.error(error);
                }
            },
            /**
             * API DELETE
             *
             * DELETE AN EXISTING EMPLOYEE
             * @param id
             */
            async deleteEmployee(id) {
                try {
                    await fetch(`https://jsonplaceholder.typicode.com/users/${id}`, {
                        method: 'DELETE'
                    });
                    this.employees = this.employees.filter(employee => employee.id !== id);
                } catch (error) {
                    console.error(error);
                }
            },
                    }
    }
</script>

<style lang="scss" scoped>
    .badge {
        background: lightblue;
        color: white;
        font-size: .5em;
        padding: .5em;
        position: relative;
        top: -.5em;
        border-radius: 50px;
    }
</style>