<template>
  <div class="home">
    <!--
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    -->
    <div class="small-container">
      <h1>Employees</h1>
      <EmployeeForm @add:employee="addEmployee" />
      <EmployeeTable :employees="employees" @delete:employee="deleteEmployee"/>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import EmployeeTable from '@/components/EmployeeTable.vue'
import EmployeeForm from "../components/EmployeeForm";


export default {
  name: 'home',
  components: {
    EmployeeForm,
    HelloWorld,
    EmployeeTable
  },
  data() {
    return {
      employees: [
        {
          id: 1,
          name: 'Richard Hendricks',
          email: 'richard@piedpiper.com',
        },
        {
          id: 2,
          name: 'Bertram Gilfoyle',
          email: 'gilfoyle@piedpiper.com',
        },
        {
          id: 3,
          name: 'Dinesh Chugtai',
          email: 'dinesh@piedpiper.com',
        },
        {
          id: 4,
          name: 'Josh Miller',
          email: 'joshmiller@gmail.com',
        },
      ],
    }
  },
  methods: {
    /**
     * CREATE A NEW EMPLOYEE
     * @param employee
     */
    addEmployee (employee) {
      const lastId =
          this.employees.length > 0
              ? this.employees[this.employees.length - 1].id
              : 0;
      const id = lastId + 1;
      const newEmployee = { ...employee, id };
      this.employees = [...this.employees, newEmployee];
    },
    /**
     * DELETE AN EXISTING EMPLOYEE
     * @param id
     */
    deleteEmployee(id) {
      this.employees = this.employees.filter(
          employee => employee.id !== id
      )
    }
  }
}
</script>
