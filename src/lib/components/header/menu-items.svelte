<script>
	export let lang;
	export let open;
	export let y;
	$: markets = false;
	$: links = false;
	const linkArr = [
		{
			url: 'https://chainz.cryptoid.info/blk/',
			title: `CryptoID ${i18n(navI18n, 'explorer', lang)}`
		},
		{
			url: `https://www.coingecko.com/${i18n(navI18n, 'locale', lang)}/coins/blackcoin`,
			title: 'Coingecko'
		},
		{
			url: 'https://coinmarketcap.com/currencies/blackcoin/#charts',
			title: 'CoinMarketCap'
		},
		{
			url: 'https://blackcoin.nl',
			title: 'BlackcoinNL'
		},
		// {
		// 	url: 'https://node.blackcoin.io/insight/',
		// 	title: `Blacksight ${i18n(navI18n, 'explorer', lang)}`
		// },
		{
			url: 'https://bitinfocharts.com/blackcoin/',
			title: `Bitinfocharts ${i18n(navI18n, 'explorer', lang)}`
		},
		{
			url: 'https://github.com/coinblack/',
			title: 'Github'
		},
		{
			url: 'https://gitlab.com/blackcoin/',
			title: 'Gitlab'
		}
	];
	import i18n from '$lib/i18n';
	import navI18n from './nav.i18n';
	const openClose = () => {
		!!links ? (links = false) : (links = true);
		// move y pos down in order to make navbar black
		y === 0 ? y = 1 : null;
	}
</script>

<ul id="main-menu">
	<li>
		<a
			on:click={() => open = !open}
			href="/{i18n(navI18n, 'locale', lang)}/#about"
		>
			{i18n(navI18n, 'about', lang)}
		</a>
	</li>
	<li>
		<a
			on:click={() => open = !open}
			href="/{i18n(navI18n, 'locale', lang)}/#downloads"
		>
			{i18n(navI18n, 'download', lang)}
		</a>
	</li>
	<li>
		<a
			on:click={() => open = !open}
			href="/{i18n(navI18n, 'locale', lang)}/donations"
		>
			{i18n(navI18n, 'donations', lang)}
		</a>
	</li>
	<li id="faq">
		<a
			on:click={() => open = !open}
			href="/{i18n(navI18n, 'locale', lang)}/faq"
		>
			<span>
				{i18n(navI18n, 'faq', lang)}
			</span>
		</a>
	</li>

	<!-- <li on:click={() => (!!markets ? (markets = false) : (markets = true))}>
        {i18n(navI18n, 'markets', lang)}
        <ul id="markets" style="display:{!!markets ? 'flex' : 'none'};">
            <button class="x">X</button>
            <a
                class="centered"
                href="https://www.coingecko.com/{i18n(navI18n, 'locale', lang)}/coins/blackcoin"
                rel="noopener"
                target="_blanknoreferer"
            >
                {i18n(navI18n, 'more_charts_on', lang)} CoinGecko
            </a>
        </ul>
    </li>
	 -->
	 <li id="linksBtn" on:click={() => openClose()} on:keydown={(e) => { if (e.key === 'Enter' || e.key === ' ') openClose() }}>
		{i18n(navI18n, 'links', lang)}
	
		<ul id="links" style="display:{!!links ? 'flex' : 'none'};">
			<button class="x" on:click={() => openClose()} on:keydown={(e) => { if (e.key === 'Enter' || e.key === ' ') openClose() }}>X</button>
			{#each linkArr as l}
				<li on:click={() => open = !open} on:keydown={(e) => { if (e.key === 'Enter' || e.key === ' ') open = !open }}>
					<a rel="noopener" target="_blank noreferer" href={l.url}>
						{l.title}
					</a>
				</li>
			{/each}
		</ul>
	</li>	
</ul>

<style>
li {
	color: #ddb77a;
	text-shadow: 1px 1px 1px orange;
}

#main-menu {
	position: absolute;
	top: 5rem;
	right: 0;
	width: 100vw;
	height: fit-content;
	display: flex;
	flex-direction: column;
	font-size: 1rem;
	line-height: 1.5rem;
	background-color: black;
	margin: 0;
	justify-content: center;
	align-content: center;
	display: flex;
	text-align: center;
}

#linksBtn {
	background-image: linear-gradient(rgba(255, 0, 0, 0.4), transparent);
	padding: 0.5rem !important;
	margin: 0 auto;
	border-radius: 5%;
}

#links {
	position: absolute;
	top: 5rem;
	justify-content: space-around;
}

#navbar ul li ul {
	flex-flow: column;
	position: relative;
	padding: 1rem;
}

#navbar ul.nav-menu > li > ul > li ul {
	left: 0%;
	top: 0px;
}

#navbar ul li ul {
	position: fixed;
	left: 0;
	background-color: #111;
	width: 100vw;
	text-align: center;
}

.x {
	background-color: transparent;
	width: fit-content;
	color: white;
	position: absolute;
	right: 1rem;
	top: 0;
	border-color: #ddb77a;
	font-size: x-large;
	padding: 0 0.75rem;
}

@media (min-width: 300px) {
	#main-menu {
		font-size: 2rem;
		line-height: 3rem;
	}

	#main-menu li {
		padding: 0 0.5rem;
	}
}

@media (min-width: 700px) {
	#main-menu {
		font-size: 4rem;
		line-height: 6rem;
	}
}

@media (min-width: 1080px) {
	#main-menu {
		position: initial;
		width: auto;
		height: auto;
		display: inline-flex;
		flex-direction: row;
		justify-content: center;
		align-content: center;
		font-size: 0.8rem;
		line-height: 1.5rem;
		background-color: transparent;
	}

	#main-menu li {
		padding: 0 0.5rem;
		align-self: center;
	}

	#linksBtn {
		padding-bottom: 1.2rem !important;
		margin: 1rem 0 0 0;
		align-self: center;
	}
	.x {
		display: none;
	}
}

@media (min-width: 1440px) {
	#main-menu {
		font-size: 1rem;
	}

	#main-menu li {
		padding: 0 0.5rem;
	}
}

@media (min-width: 2560px) {
	#main-menu {
		font-size: 1.75rem;
	}

	#main-menu li {
		padding: 0 1.5rem;
		font-size: 1rem;
	}
}

</style>
