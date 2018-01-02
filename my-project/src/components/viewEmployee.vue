<template>
    <div id= 'view-employee'>
        <ul class="collection with-header">

            <li class="collection-header">
                <h4>{{name}}</h4>
            </li>
        </ul>
    </div>
</template>

<script>
import db from './firebaseinit'
export default{

    name: 'view-employee',
    data(){
        return{
            emp_id: null,
            name:null,
            location:null

        }
        
    },
    beforeRouteEnter(to,from,next){
        
        db.collection('employees').where('id','==',to.params.id).get().then(
            querySnapshot=>{
                
                querySnapshot.forEach(doc=>{
                        next(vm=>{
                            vm.emp_id = doc.data().id,
                            vm.name = doc.data().name,
                            vm.location = doc.data().location
                        })
                })
            }
        )
    },
    watch:{
        '$route':'fetchData'
    },
    methods:{
        fetchData(){
            db.collection('employees').where('id','==', this.$route.params.id).get().then(
                querySnapShot => {
                    querySnapShot.forEach(doc=> {
                        this.emp_id= doc.data().id,
                        this.name=doc.data().name 
                    })
                }
            )
        }
    }
}

</script>