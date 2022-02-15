<script lang="ts">
	import { getAuth as auth, GoogleAuthProvider, signInWithPopup } from 'firebase/auth';
	import { user } from '../../store/authStore';

	import {
		Header,
		HeaderUtilities,
		SkipToContent,
		HeaderAction,
		HeaderPanelLinks,
		HeaderPanelDivider,
		HeaderPanelLink
	} from 'carbon-components-svelte';
	import UserAvatarFilledAlt20 from 'carbon-icons-svelte/lib/UserAvatarFilledAlt20';

	let isOpen1 = false;

	const login = async (provider) => {
		await signInWithPopup(auth(), provider);
	};

	function loginWithGoogle() {
		const googleProvider = new GoogleAuthProvider();
		login(googleProvider);
	}

	function logout() {
		auth().signOut();
	}
</script>

<Header platformName="Bidoku">
	<svelte:fragment slot="skip-to-content">
		<SkipToContent />
	</svelte:fragment>

	<HeaderUtilities>
		<HeaderAction
			bind:isOpen={isOpen1}
			icon={UserAvatarFilledAlt20}
			closeIcon={UserAvatarFilledAlt20}
		>
			<HeaderPanelLinks>
				{#if $user}
					{#if $user.photoURL}
						<HeaderPanelDivider>
							<img src={$user.photoURL} width="60" height="60" alt="" />
						</HeaderPanelDivider>
					{/if}

					<HeaderPanelLink>Profil</HeaderPanelLink>
					<HeaderPanelLink>Yüklemelerim</HeaderPanelLink>
					<HeaderPanelLink on:click={logout}>Çıkış Yap</HeaderPanelLink>
				{:else}
					<HeaderPanelDivider>Giriş Yap</HeaderPanelDivider>
					<HeaderPanelLink on:click={loginWithGoogle}>Google</HeaderPanelLink>
				{/if}
			</HeaderPanelLinks>
		</HeaderAction>
	</HeaderUtilities>
</Header>
