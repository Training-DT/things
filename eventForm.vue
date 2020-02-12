 <template>
    <div id="app" class="container">
        <div class="page-header">
            <h1>Vue.js & Firebase <small>Fetch info</small></h1>
        </div>

        <select id="idol" v-on:click="loadIdol()" >
            <option value="select">Please Select Idol</option>
            <option  v-for="(idol) in idols" v-bind:key="idol.id">{{idol.name}}</option>
        </select> 
        <br><br>
        <select id="location" v-on:click="loadLocation()" >
            <option value="select">Please Select Location</option>
            <option  v-for="(location) in locations" v-bind:key="location.id">{{location.locationName}}</option>
        </select> 
                        
        
        </div>
</template>

<!--firebase config-->
<script src="https://www.gstatic.com/firebasejs/7.7.0/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/7.7.0/firebase-firestore.js"></script>

<script>
    import { firebase } from "@firebase/app";
    import "@firebase/firestore";
       
    var firebaseConfig = {
        apiKey: "AIzaSyAJGizlnRRufuCoI4PDaH7Zi9mxyrVBOXQ",
        authDomain: "mrtproject-386ae.firebaseapp.com",
        databaseURL: "https://mrtproject-386ae.firebaseio.com",
        projectId: "mrtproject-386ae",
        storageBucket: "mrtproject-386ae.appspot.com",
        messagingSenderId: "392425188189",
        appId: "1:392425188189:web:9e8457bd7800515f2c96b4"
    };

    firebase.initializeApp(firebaseConfig);
    const db = firebase.firestore(); 

    export default{
        data() {
            return {
                event:[],
                locations:'',
                idols:'' 
            }
        },
        firebase(){
            return{
                idols:db.collection('Person'),
                locations:db.collection('Locations')
            }
        },
        methods:{
            loadIdol() {
                let idolList = [];
                console.log("Hello");
                db.collection('Person').get().then(function(querySnapshot) {
                    querySnapshot.forEach(function(doc) {  
                        console.log(doc.id)
                    let idol = {
                        id: doc.id,
                        name: doc.data().name,
                    }
                    idolList.push(idol)
                    });
                });
                this.idols = idolList;
            },
            loadLocation() {
                let locationList = [];
                console.log("Hello");
                db.collection('Locations').get().then(function(querySnapshot) {
                    querySnapshot.forEach(function(doc) {  
                        console.log(doc.id)
                    let location = {
                        id: doc.id,
                        locationName: doc.data().locationName,
                    }
                    locationList.push(location)
                    });
                });
                this.locations = locationList;
            },
                    
        }
    }
</script>

<style>
    @import url("https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css");
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 20px;
}
</style>