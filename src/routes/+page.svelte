<svelte:head>
	<link rel="stylesheet" href="style.css" />
</svelte:head>

<script>
	import CharacterSelector from '../components/personData.svelte';

  let selectedCharacter = null;

  function handleCharacterClick(character) {
    selectedCharacter = character;
  }

  import { onMount } from 'svelte';

onMount(async () => {
	// JavaScript om klikgebeurtenissen aan de afbeeldingen toe te voegen
	const characterList = document.querySelector('ul');
    const characterClick = document.querySelector('.harryClick');
    let currentStaandAfbeelding = null;

	// Mapping van karakternamen naar bijbehorende staande afbeeldingen
    const staandeAfbeeldingen = {
      'harry': 'harrypotterstaand.png',
      'hermelien': 'hermelienstaand.png',
      'ron': 'ronstaand.png',
      'neville': 'nevillestaand.png',
	  'draco': 'dracostaand.png',
      'sirius': 'siriusstaand.png',
      'sneep': 'snapestaand.png',
    };

	characterList.addEventListener('click', function (event) {
		if (event.target.tagName === 'IMG') {
			const karakterNaam = event.target.classList[0]; // Neem de klasse van het geklikte karakter

			// Controleer of de geklikte afbeelding al wordt weergegeven
			if (staandeAfbeeldingen[karakterNaam] === currentStaandAfbeelding) {
			// Als het dezelfde afbeelding is, laat deze verdwijnen
			characterClick.innerHTML = '';
			currentStaandAfbeelding = null;
			} else {
			// Als het een andere afbeelding is, laat deze zien
			toonStaandeAfbeelding(staandeAfbeeldingen[karakterNaam]);
			currentStaandAfbeelding = staandeAfbeeldingen[karakterNaam];
			}
		}
		});

		    // JavaScript-functie om de staande afbeelding weer te geven
			function toonStaandeAfbeelding(staandeAfbeelding) {
      // Verander de HTML van het element om de staande afbeelding weer te geven
      characterClick.innerHTML = `<img src="../images/${staandeAfbeelding}" alt="Staande afbeelding">`;
    }
  });

</script>

<main>
	<h1>Choose your character</h1>

		<ul>
			<li><img class="harry" src="images/harry.png" alt="harry potter"></li>
			<li><img class="hermelien" src="images/hermelien.png" alt="harry potter"></li>
			<li><img src="images/ron.png" alt="harry potter"></li>
			<li><img src="images/neville.png" alt="harry potter"></li>
			<li><img src="images/draco.png" alt="harry potter"></li>
			<li><img src="images/sirius.png" alt="harry potter"></li>
			<li><img src="images/sneep.png" alt="harry potter"></li>
		</ul>

		<div class="harryClick"></div>
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