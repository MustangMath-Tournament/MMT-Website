<script>
	import Header from '$lib/header/Header.svelte';
	import SocialsLink from '$lib/components/SocialsLink.svelte';
	import '../app.css';
    import { page } from "$app/stores";
	import Newsletter from '$lib/components/Newsletter.svelte';
	import { user } from '$lib/store';
	import { onMount } from "svelte";
	import { inject } from '@vercel/analytics'

	//inject({ mode: dev ? 'development' : 'production' });

	let show = false;

	onMount(() => {
        user.subscribe((u) => (show = u));
    })
</script>
<head><!-- Google Tag Manager -->
	<script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
	new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
	j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
	'https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
	})(window,document,'script','dataLayer','GTM-59ZGZS8');</script>
	<!-- End Google Tag Manager -->
</head>
<body>
	<!-- Google Tag Manager (noscript) -->
<noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-59ZGZS8"
	height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
	<!-- End Google Tag Manager (noscript) -->
<div class="all-container">
    <Header />

	<main>
		<slot />
		<Newsletter show={show} />
	</main>

	<footer>
		<div class="socials">
			<button class="sign-up" on:click={() => {show = !show;}}><i class="fa-regular fa-newspaper"></i> Signup</button>
			<div class="divider"></div>
			<SocialsLink url="mailto:contact@mustangmath.com" type="solid" icon="envelope" />
			<SocialsLink url="https://discord.gg/bYDDWxan5d" type="brands" icon="discord" />
			<SocialsLink url="https://www.facebook.com/MustangMath" type="brands" icon="facebook" />
			<SocialsLink url="https://www.instagram.com/mustangmath/" type="brands" icon="instagram" />
			<SocialsLink url="https://www.linkedin.com/company/mustangmathtournament/" type="brands" icon="linkedin"/>
			<SocialsLink url="https://www.youtube.com/channel/UCCCk-s3dHatOKfwiC5yJBAA" type="brands" icon="youtube"/>
			<SocialsLink url="https://artofproblemsolving.com/wiki/index.php/Mustang_Math_Tournament" type="text" icon="AoPS" text />
		</div>
	</footer>
</div>
</body>

<style>
	.divider {
		width: 2px;
		background-color: white;
		height: 50px;
		margin-left: 10px;
	}

	@media screen and (max-width: 900px) {
		.divider {
			margin-right: 5px;
		}
	}

	main {
		flex: 1;
		display: flex;
		flex-direction: column;
		width: 100%;
		margin: 0 auto;
		box-sizing: border-box;
	}

	.all-container {
		position: relative;
		min-height: 100vh;
		box-sizing: border-box;
		margin-bottom: 10vh;
	}

	footer {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		bottom: 0;
		width: 100%;
		text-align: center;
		position: fixed;
		z-index: 2;
		min-height: 50px;
		background-color: #1c6825;
	}

	.socials {
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: center;
		font-size: 1.5rem;
		padding-top: 10px;
		padding-bottom: 8px;
	}
</style>
