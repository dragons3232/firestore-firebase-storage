<script lang="ts">
	import {
		addDoc,
		arrayUnion,
		collection,
		deleteDoc,
		deleteField,
		updateDoc
	} from 'firebase/firestore';
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

	const deleteAlbum = async (album) => {
		console.log(album);
		deleteDoc(album.ref);
	};

	const deleteAlbumField = async (album) => {
		console.log(album);
		updateDoc(album.ref, {
			desc: deleteField()
		});
	};

	const addSong = async (album) => {
		updateDoc(album.ref, {
			songs: arrayUnion({
				name: 'Song' + new Date().getTime(),
				desc: 'Song Description',
				date: new Date()
			})
		});
	};
</script>

{#each $data as album}
	<p>{album.name}</p>
	<p>{album.desc}</p>
	<p>{album.date}</p>
	<p>{new Date(album.date.seconds * 1000)}</p>

	<button on:click={() => deleteAlbum(album)}>Delete Album</button>
	<button on:click={() => addSong(album)}>Add song</button>
	<button on:click={() => deleteAlbumField(album)}>Delete field</button>
{/each}

<button on:click={addAlbum}>Add Album</button>
