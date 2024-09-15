<script lang="ts">
	import { Collection } from 'sveltefire';
</script>

<Collection ref={'albums'} let:data let:count>
	<p>Found {count} albums</p>

	{#each data as album}
		<p>{album.name}</p>
		<p>{album.desc}</p>
		<p>{album.date}</p>
		<p>{new Date(album.date.seconds * 1000)}</p>
	{/each}

	<p slot="loading">Loading...</p>
</Collection>
