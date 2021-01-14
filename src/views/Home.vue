<template>
  <div class="home">
    <div v-for="pet in this.pets" :key="pet.id" :style="parent">
      <div class="card" :style="cardStyle">
        <img :src="pet.primary_photo_cropped.small" alt="Avatar" :style="image">
        <div class="container" :style="container">
          <h4><b>{{pet.name}}</b></h4>
          <p>{{pet.breeds.primary}}</p>
          <ul>
            <li>{{pet.contact.address.city}},{{pet.contact.address.state}}</li>
            <li>{{pet.contact.email}}</li>
          </ul>
        </div>
      </div>  

    </div>
  </div>
</template>

<script>
import dotenv from 'dotenv';
dotenv.config()
export default {
  name: 'Home',
  data(){
    return {
      pets: {},
      parent: { margin: "auto", width: "60%"},
      cardStyle: { 
        boxShadow: "0 4px 8px 0 rgba(0,0,0,0.2)",
        transition: "0.3s",
        borderRadius: "5px",
        display: "flex"
        },
      container: { padding: "2px 16px"},
      image: {borderRadius: "5px 5px 0 0",
      maxHeight: "200px",
      maxWidth: "200px"}
    }
  },
  components: {
  },
    created() {
      var org = 'RI77';
      var status = 'adoptable';
    // POST request using fetch with error handling
    fetch('https://api.petfinder.com/v2/oauth2/token', {
	method: 'POST',
	body: 'grant_type=client_credentials&client_id=' + process.env.VUE_APP_PETFINDER_API_KEY + '&client_secret=' + process.env.VUE_APP_PETFINDER_SECRET,
	headers: {
		'Content-Type': 'application/x-www-form-urlencoded'
	}
}).then(function (resp) {

	// Return the response as JSON
	return resp.json();

}).then(function (data) {

	return fetch('https://api.petfinder.com/v2/animals?organization=' + org + '&status=' + status, {
		headers: {
			'Authorization': data.token_type + ' ' + data.access_token,
			'Content-Type': 'application/x-www-form-urlencoded'
		}
	});

}).then(function (resp) {

	// Return the API response as JSON
	return resp.json();

}).then((data) => {

	// Log the pet data
  this.pets = data.animals
  console.log(data)

}).catch(function (err) {

	// Log any errors
	console.log('something went wrong', err);

});
}}
</script>
