<script lang="ts">
	import { getAuth as auth, GoogleAuthProvider, signInWithPopup } from 'firebase/auth';
	import { user } from '../../store/authStore';

	async function loginWithGoogle() {
		const provider = new GoogleAuthProvider();
		await signInWithPopup(auth(), provider);
	}
</script>

<h1>Header</h1>
<button on:click={loginWithGoogle}>Google</button>
{#if $user}
	<p>Hello, {$user.displayName}</p>
	<button on:click={() => auth().signOut()}>Logout</button>
{/if}
