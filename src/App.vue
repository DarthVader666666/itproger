<template>
    <input type="text" v-model="userName" placeholder="Name">
    <input type="password" v-model="userPass" placeholder="Password">
    <input type="email" v-model="userEmail" placeholder="Email">

    <p className="error">{{ error }}</p>
    <button type="button" @click="sendData()">Send</button>

    <div v-if="users.length == 0" className="user">
      No users in stock
    </div>
    <div v-else-if="users.length > 1" className="user">
      Users count: {{ this.users.length }}
    </div>
    <div v-else className="user">
      One user in stock
    </div>

    <User v-for="(el, index) in users" :key="index" :user="el" :index="index" :deleteUser="deleteUser"></User>

    
</template>

<script>
  import User from './components/User.vue'

  export default{
    components: {User},

    data() {
      return {
        users:[],
        error:'',
        userName:'',
        userPass:'',
        userEmail:''
      }
    },
    methods: {
      sendData() {
        if(this.userName == '') {
            this.error = "Please, enter Name";
            return;
        }
        else if(this.userEmail == '')
        {
            this.error = "Please, enter Email";
            return;
        }
        else if(this.userPass == '')
        {
            this.error = "Please, enter Password";
            return;
        }

        this.error = '';

        this.users.push(
          {
            name: this.userName,
            pass: this.userPass,
            email: this.userPass
          })
      },

      deleteUser(index)
      {
        this.users.splice(index, 1);
      }
    }
  }
</script>

<style scoped>
  input {
    display: block;
    margin-bottom: 10px;
    border-radius: 3px;
    border: 1px solid silver;
    outline: none;
    padding: 10px 15px;
    background: #fafafa;
    color: #333;
  }

  button {
    border: 0;
    border-radius: 5px;
    outline: none;
    padding: 10px 15px;
    background: #6cd670;
    color: #167f3d;
    font-weight: bold;
    cursor: pointer;
    transition: transform 500ms ease;
  }

button:hover {
  transform: translateY(-5px);
}



</style>