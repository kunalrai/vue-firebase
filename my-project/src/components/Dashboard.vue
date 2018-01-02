<template>
    <div id= 'dashboard'>
        <h3>Dashboard</h3>
            <ul class="collection with-header">
                <li class="collection-header">
                    <h4>Employee</h4>
                </li>
                <li v-for="employee in employees"
                    v-bind:key="employee.emp_id" class="collection-item">
                    <div class="chip">{{employee.location}}</div>
                    {{employee.name}}
                </li>

            </ul>
        <div class="fixed-action-btn">
            <router-link to=/new class="btn-floating btn-large red">
            <i class="fa fa-plus"></i></router-link>
        </div>
    </div>
</template>


<script>
import db from './firebaseinit'
export default{

    name: 'dashboard',
    data(){
        return{
            employees:[]
            
        }
    },
    created(){
        db.collection('employees').get().then
        (querySnapshot => {querySnapshot.forEach(doc=> {
            //console.log(doc.data());
            const data = {
                    'id':doc.id,
                    'emp_id':doc.data().id,
                    'location':doc.data().location,
                    'job_title':doc.data().job_title,
                    'name': doc.data().name
                }
                this.employees.push(data);
            })
        })
    }
}

</script>