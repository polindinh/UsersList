<template>
    <div class="container" >
        <p @click="getUsers">Click me for users </p>
        <h3 id="user-name" v-for="user in users" :key="user.id" >{{user.name}}</h3>
    </div>
</template>

<script>
    export default {
        data: function(){
            return{
                users:[],
            };
        },
        methods:{
            getUsers: function(){
                let compData = this;
                let ajax = new XMLHttpRequest;
                ajax.onreadystatechange = (function(){
                    if(ajax.status == 200 && ajax.readyState == 4){
                        let jsonData = JSON.parse(this.responseText);
                        console.log(this.responseText);
                        //compData.users = jsonData.users; all ready an array
                        compData.users = jsonData;
                        console.log(compData.users);

                    }
                });
                ajax.open('GET','/get-users', true);
                ajax.send();
            }
        },

    }
</script>
