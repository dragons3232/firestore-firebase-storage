<script lang="ts">
	import { FirebaseApp } from 'sveltefire';
	import { initializeApp } from 'firebase/app';
	import { getFirestore } from 'firebase/firestore';
	import { getAuth } from 'firebase/auth';

	const firebaseConfig = {
		apiKey: 'AIzaSyA2BVU4dhYsk2A-9K6gmgSWVBRUi-_h5BE',
		authDomain: 'firestoresvelte.firebaseapp.com',
		projectId: 'firestoresvelte',
		storageBucket: 'firestoresvelte.appspot.com',
		messagingSenderId: '625074932962',
		appId: '1:625074932962:web:7ebf59d2c6fcfb77bba2bb'
	};
	// Initialize Firebase
	const app = initializeApp(firebaseConfig);
	const firestore = getFirestore(app);
	const auth = getAuth(app);
</script>

<FirebaseApp {auth} {firestore}>
	<slot />
</FirebaseApp>
