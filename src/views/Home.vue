<template>
  <div class="home">
    <!--
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    -->
    <div class="small-container">
      <h1>Employees</h1>
      <EmployeeForm @add:employee="addEmployee" />
      <EmployeeTable :employees="employees"/>
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
          name: 'Richard Hendricks',
          email: 'richard@piedpiper.com',
        },
        {
          name: 'Bertram Gilfoyle',
          email: 'gilfoyle@piedpiper.com',
        },
        {
          name: 'Dinesh Chugtai',
          email: 'dinesh@piedpiper.com',
        },
        {
          name: 'Josh Miller',
          email: 'joshmiller@gmail.com',
        },
      ],
    }
  },
  methods: {
    addEmployee (employee) {
      alert('Employee Added');

      const newEmployee = { ...employee};

      this.employees = [...this.employees, newEmployee];
    }
  }
}
</script>
