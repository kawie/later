<script>
	import ImageInput from './ImageInput.svelte';
</script>

<script context="module">
  export const load = async ({ session, fetch }) => {
    // Only run the service worker registration on the client side
    if (typeof window !== 'undefined' && 'serviceWorker' in navigator) {
      navigator.serviceWorker.register('/service-worker.js').then(() => {
        console.log('Service Worker registered');
      }).catch((error) => {
        console.error('Service Worker registration failed:', error);
      });
    }
  };
</script>

<svelte:head>
	<title>Latest</title>
	<meta name="description" content="My first SvelteKit app" />
	<link rel="manifest" href="/manifest.json" />
	<meta name="theme-color" content="#cad8e4" />
</svelte:head>

<section>
	<ImageInput />
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}
</style>
