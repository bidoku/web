<script lang="ts">
	import 'carbon-components-svelte/css/white.css';

	import { onMount } from 'svelte';
	import { getAuth as auth } from 'firebase/auth';
	import '$lib/firebase';

	import Header from '../components/layout/Header.svelte';
	import Footer from '../components/layout/Footer.svelte';
	import { Content } from 'carbon-components-svelte';

	import { user, loggedIn } from '../store/authStore';

	onMount(() => {
		auth().onAuthStateChanged((authenticatedUser) => {
			loggedIn.set(user !== null);
			user.set(authenticatedUser);
		});
	});
</script>

<svelte:head>
	<title>Bidoku</title>
</svelte:head>

<Header />
<Content>
	<slot />
</Content>
<Footer />
