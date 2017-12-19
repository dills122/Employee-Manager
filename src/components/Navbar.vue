<template>
	<div class="nav-bar blue">
		<router-link to="/login" class="brand-logo" v-if="authed === false">
			<i class="icon ion-android-settings"></i>
			Login
		</router-link>
		<a href="" v-if="authed" class="brand-logo">
			<i class="icon ion-android-settings"></i>
			Log off
		</a>
		<router-link to="/" class="brand-logo">
			<i class="icon ion-ios-home"></i>
			Home
		</router-link>
		<router-link to="/new" class="brand-logo">
			<i class="icon ion-android-add"></i>
			New Employee
		</router-link>
	</div>
</template>
<style type="text/css">
.nav-bar {
	width: 100%;
	height: 2em;
	color: #FFF;
	line-height: 2em;
}

.nav-bar a {
	padding: .25em;
	margin-right: 1.5em;
	color: #FFF;
}
.nav-bar a:hover {
	padding: .25em;
	color: #CCC;
}

</style>

<script type="text/javascript">
import firebase from 'firebase'
export default {
	name: 'nav-bar',
	data () {
		return {
			authed: false
		}
	},
	created() {
		var user = firebase.auth().currentUser;

		if (user) {
			this.authed = true;
		}
	}
}
</script>