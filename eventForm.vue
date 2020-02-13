 <template>
    <div id="app" class="container">
        <div class="page-header">
            <h1>Vue.js & Firebase <small>Fetch info</small></h1>
        </div>
        <h5>Idol</h5>
        <select v-model="selectedIdol" id="idol" v-on:click="loadIdol()" >
            <option value="null">Please Select Idol</option>
            <option  v-for="(idol) in idols" v-bind:key="idol.id" value:key="idol.name">{{idol.name}}</option>
        </select>
        <br><br>
        <h5>Location</h5>
        <select v-model="selectedLocation" id="location" v-on:click="loadLocation()" >
            <option value="null">Please Select Location</option>
            <option  v-for="(location) in locations" v-bind:key="location.id" value:key="location.locationName">{{location.locationName}}</option>
        </select>
        <br><br>
        <h5>Start Date</h5>
        <select v-model="selectedStartDate" id="location" v-on:click="loadLocation()" >
            <option value="null">Please Select Start Date</option>
            <option  v-for="(location) in locations" v-bind:key="location.id" value:key="location.locationName">{{location.locationName}}</option>
        </select>
        <br><br>
        <h5>End Date</h5>
        <select v-model="selectedEndDate" id="location" v-on:click="loadLocation()" >
            <option value="null">Please Select End Date</option>
            <option  v-for="(location) in locations" v-bind:key="location.id" value:key="location.locationName">{{location.locationName}}</option>
        </select>
        <br><br>
        <h3>Result</h3>
        <div class="mt-2">Idol: <strong>{{ selectedIdol }}</strong></div>         
        <div class="mt-2">Location: <strong>{{ selectedLocation }}</strong></div>

        <button type="button" class="btn btn-info" v-on:click="loadTodo()">  Add Event </button><br><br>
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
                events:[],
                locations:'',
                idols:'' ,
                selectedIdol: null,
                selectedLocation: null,
                selectedStartDate: null,
                selectedEndDate: null
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
            selectLocation(collectionID) {
                
            }
                    
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