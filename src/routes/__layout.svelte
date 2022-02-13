<script lang="ts">
	import { onMount } from 'svelte';
	import { initFirebase } from '$lib/initFirebase';
	import Header from '../components/layout/Header.svelte';
	import { getAuth as auth } from 'firebase/auth';

	import { user, loggedIn } from '../store/authStore';

	onMount(() => {
		initFirebase();

		auth().onAuthStateChanged((authenticatedUser) => {
			loggedIn.set(user !== null);
			user.set(authenticatedUser);
		});
	});
</script>

<Header />
<slot />
