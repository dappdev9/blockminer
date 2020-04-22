<script>
	import Auth from './components/Auth.svelte';
	import Home from './Home.svelte';

	import firebase from 'firebase/app';
	import 'firebase/auth';
	import 'firebase/firestore';

	import {FirebaseApp, User} from 'sveltefire';

	const firebaseConfig = {
		apiKey: "AIzaSyArIMi-upcXalA4CJYcgIYr53pNhxWtST0",
		authDomain: "blockmainer.firebaseapp.com",
		databaseURL: "https://blockmainer.firebaseio.com",
		projectId: "blockmainer",
		storageBucket: "blockmainer.appspot.com",
		messagingSenderId: "8228077292",
		appId: "1:8228077292:web:e7aa88bdb8519de0e6afc9"
	};
	
	firebase.initializeApp(firebaseConfig);

</script>

<FirebaseApp {firebase}>
	<User let:user let:auth>
		<div slot="signed-out">
			<Auth {auth}/>
		</div>
		<div>
			<Home {user} {auth} {firebase}/>
		</div>
	</User>
</FirebaseApp>
