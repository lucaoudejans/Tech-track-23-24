<svelte:head>
	<link rel="stylesheet" href="style.css" />
</svelte:head>

<script>
	import CharacterSelector from '../components/personData.svelte';

  let selectedCharacter = null;

  function handleCharacterClick(character) {
    selectedCharacter = character;
  }
</script>

<main>
	<h1>Choose your charachter</h1>

		<ul>
			<li><img src="images/harry.png" alt="harry potter"></li>
			<li><img src="images/hermelien.png" alt="harry potter"></li>
			<li><img src="images/ron.png" alt="harry potter"></li>
			<li><img src="images/neville.png" alt="harry potter"></li>
			<li><img src="images/draco.png" alt="harry potter"></li>
			<li><img src="images/sirius.png" alt="harry potter"></li>
			<li><img src="images/sneep.png" alt="harry potter"></li>
		</ul>
</main>

<style>
	h1 {
		text-align: center;
		font-family:Verdana, Geneva, Tahoma, sans-serif;
	}

	ul {
		list-style: none;
		display: flex;
		flex-direction: row;
		justify-content: center;
		padding: 5em;
		cursor: pointer;
	}

	img {
		width: 7em;
	}
</style>

<CharacterSelector />