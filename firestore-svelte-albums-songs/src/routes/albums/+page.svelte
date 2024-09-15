<script lang="ts">
	import { addDoc, collection } from 'firebase/firestore';
	import { getFirebaseContext, collectionStore } from 'sveltefire';
	const { auth, firestore, storage, rtdb, analytics } = getFirebaseContext();

	const data = collectionStore(firestore, 'albums');
	const albumCollection = collection(firestore, 'albums');

	const addAlbum = async () => {
		await addDoc(albumCollection, {
			name: 'Album' + new Date().getTime(),
			desc: 'Album Description',
			date: new Date()
		});
	};
</script>

{#each $data as album}
	<p>{album.name}</p>
	<p>{album.desc}</p>
	<p>{album.date}</p>
	<p>{new Date(album.date.seconds * 1000)}</p>
{/each}

<button on:click={addAlbum}>Add Album</button>
