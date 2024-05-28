<template>
    <div className="user">
        <button @click="deleteUser(index)">Delete</button>
        <h3>{{ user.name }}</h3>
        <p>{{ user.email }} - <b>{{ user.pass }}</b></p>
    </div>    
</template>

<script>

export default{
    props:{
        user:{
           type: Object,
           required: true
        },
        index:{
            type: Number,
            required: true
        },
        deleteUser:{
            type:Function,
            required: true
        }
    }
}
</script>

<style>
    .user {
      width: 500px;
      margin-top: 20px;
      border: 1px solid silver;
      background: #e3e3e3;
      color: #222;
      padding: 20px;
      border-radius: 5px;
    }
</style>