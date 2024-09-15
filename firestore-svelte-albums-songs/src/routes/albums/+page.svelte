<script lang="ts">
	import { getFirebaseContext, collectionStore } from 'sveltefire';
	const { auth, firestore, storage, rtdb, analytics } = getFirebaseContext();

	const data = collectionStore(firestore, 'albums');
</script>

{#each $data as album}
	<p>{album.name}</p>
	<p>{album.desc}</p>
	<p>{album.date}</p>
	<p>{new Date(album.date.seconds * 1000)}</p>
{/each}
