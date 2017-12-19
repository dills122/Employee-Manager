<template>
  <div id="home">
    <ul class="collection with-header">
      <li class="collection-header"><h4>Employees</h4></li>
      <li v-for="employee in employees" v-bind:key="employee.id" class="collection-item">
        <div class="chip">{{employee.dept}}</div>
        {{employee.employee_id}}: {{employee.name}} 
         <router-link class="secondary-content" v-bind:to="{ name: 'view-employee', params: { employee_id: employee.employee_id }}"><i class="icon ion-eye"></i></router-link>
      </li>
    </ul>
  </div>
</template>

<script>
  import db from './firebaseInit'
  import firebase from 'firebase'
  export default {
    name: 'home',
    data () {
      return {
        employees: [],
        loading: true,
        authed: false
      }
    },
    created () {
      db.collection('employees').orderBy('dept').get().then((querySnapshot) => {
        this.loading = false
        querySnapshot.forEach((doc) => {
          const data = {
            'id': doc.id,
            'employee_id': doc.data().employee_id,
            'name': doc.data().name,
            'dept': doc.data().dept,
            'position': doc.data().position
          }
          this.employees.push(data)
        })
      })
      this.checkUser();
    },
    methods: {
      checkUser() {
        firebase.auth().onAuthStateChanged(firebaseUser => {
          if(firebaseUser) {
            console.log(firebaseUser);
            this.authed = true;
          } else {
            console.log('not logged in');
            this.authed = false;
          }
        });
      }
    }
  }
</script>