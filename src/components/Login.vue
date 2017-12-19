  <template>
  <div class="container">
      <div class="row">

          <div class="col s6 offset-s3 z-depth-1 panel" id="panell">
            <div class="center">
                <h5 class="title">Login Form</h5>
            </div>
            <form @submit.prevent="login">
                <div class="input-field" id="username">
                  <input  type="text" class="validate" v-model="username" placeholder="Username" required>
                  <label for="username"></label>
              </div>
              <div class="input-field" id="password" >
                <input  type="password" class="validate" v-model="password" placeholder="Password" required>
                <label for="password"></label>
            </div>
            <p>
                <input type="checkbox" id="remember"  />
                <label for="remember" id="checkbox" >Remember me</label>
            </p>
            <div class="btn-container">
                <button type="submit" class="waves-effect waves-light btn login-btn blue">Login</button>
                <a class="waves-effect waves-light btn signup-btn blue" id="sign-up">Sign Up</a>
            </div>
        </form>
    </div>
  </div>

  </div>
  </template>
  <style type="text/css">

  .panel{
   margin-top: 100px;
   padding: 0px;
  }
  .login-btn{
   float: right;
   margin-bottom: 10px;
  }
  .signup-btn {
   float: left;
   margin-bottom: 10px;
  }
  .btn-container {
    margin-bottom: 10px;

  }
  form{
   padding:0px;
   border-radius: 3px;
   box-sizing: border-box;
  }
  #username,#password{
    margin-left: 20px;
    margin-right: 20px;
  }
  #checkbox{
    margin-left: 30px;
  }
  </style>
  <script>
  import firebase from 'firebase'

  export default {
    name: "login",
    data() {
      return {
        username: null,
        password: null,
        authed: false
      }
    },
    created() {
      this.CheckAuth();
    },
    methods: {
        login() {
          const promise = firebase.auth().signInWithEmailAndPassword(this.username, this.password); 
          promise.catch(e => console.log(e.message));
        },
        CheckAuth() {
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