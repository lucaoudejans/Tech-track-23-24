<!-- This project is made by Luca Oudejans in association with ChatGPT, resources and the teachers from tech track. 
The resources can be found in my Wiki! -->
<!-- Linking stylesheet -->
<svelte:head>
	<link rel="stylesheet" href="style.css" />
</svelte:head>

<!-- importing onmount and components -->
<script>
import { onMount } from 'svelte';
import Barchart from '../components/Barchart.svelte';
import Dotplot from '../components/Dotplot.svelte';

// set characters value to null
  let selectedCharacterHarryData = null;
  let selectedCharacterHermioneData = null;
  let selectedCharacterRonData = null;
  let selectedCharacterNevilleData = null;
  let selectedCharacterDracoData = null;
  let selectedCharacterSiriusData = null;
  let selectedCharacterSnapeData = null;

  
  onMount(async () => {
// filtered specific characters from the dataset
    try {
		const desiredCharacters = ['Harry Potter', 'Hermione Granger', 'Ron Weasley', 'Draco Malfoy', 'Neville Longbottom', 'Severus Snape', 'Sirius Black'];
// fetching the dataset
	const response = await fetch('https://hp-api.onrender.com/api/characters');
	const data = await response.json();

	const filteredCharacters = data.filter(character => desiredCharacters.includes(character.name));

// to check if the specific characters have been filtered
	console.log('Gefilterde karakters:', filteredCharacters);

// adding value to the characters (data)
	selectedCharacterHarryData = filteredCharacters.find(character => character.name === 'Harry Potter');
	selectedCharacterHermioneData = filteredCharacters.find(character => character.name === 'Hermione Granger');
	selectedCharacterRonData = filteredCharacters.find(character => character.name === 'Ron Weasley');
	selectedCharacterNevilleData = filteredCharacters.find(character => character.name === 'Neville Longbottom');
	selectedCharacterDracoData = filteredCharacters.find(character => character.name === 'Draco Malfoy');
	selectedCharacterSiriusData = filteredCharacters.find(character => character.name === 'Sirius Black');
	selectedCharacterSnapeData = filteredCharacters.find(character => character.name === 'Severus Snape');

// to check if it's fetched correctly
	console.log('Geselecteerde karakters:', selectedCharacterHarryData, selectedCharacterHermioneData, selectedCharacterRonData, selectedCharacterNevilleData, selectedCharacterDracoData, selectedCharacterSiriusData, selectedCharacterSnapeData);
	} catch (error) {
	console.error('Er was een probleem met de fetch-operatie:', error);
	}

// scroll function
    function scrollToSection(targetClass) {
      const targetSection = document.querySelector(`.${targetClass}`);

      if (targetSection) {
        targetSection.scrollIntoView({ behavior: 'smooth' });
      }
    }

// scroll to section when clicked on button
	const button = document.querySelector('button');

	if (button) {
      button.addEventListener('click', () => {
        scrollToSection('graphicssection');
      });
    }

// Event listener for Harry
    document.querySelectorAll('.harry').forEach((harryElement) => {
      harryElement.addEventListener('click', () => {
        scrollToSection('harrysection');
      });
    });

// Event listener for Hermelien
    document.querySelectorAll('.hermelien').forEach((hermelienElement) => {
      hermelienElement.addEventListener('click', () => {
        scrollToSection('hermionesection');
      });
    });

// Event listener for Ron
		document.querySelectorAll('.ron').forEach((ronElement) => {
      ronElement.addEventListener('click', () => {
        scrollToSection('ronsection');
      });
    });

// Event listener for Neville
		document.querySelectorAll('.neville').forEach((nevilleElement) => {
      nevilleElement.addEventListener('click', () => {
        scrollToSection('nevillesection');
      });
    });

// Event listener for Draco
		document.querySelectorAll('.draco').forEach((dracoElement) => {
      dracoElement.addEventListener('click', () => {
        scrollToSection('dracosection');
      });
    });

// Event listener for Sirius
		document.querySelectorAll('.sirius').forEach((siriusElement) => {
      siriusElement.addEventListener('click', () => {
        scrollToSection('siriussection');
      });
    });

// Event listener for Snape
		document.querySelectorAll('.snape').forEach((snapeElement) => {
      snapeElement.addEventListener('click', () => {
        scrollToSection('snapesection');
      });
    });

// Scroll back butto 
	const goBackButton = document.querySelector('.goBackButton');

		if (goBackButton) {
			goBackButton.addEventListener('click', () => {
				scrollToSection('charactersection');
			});
		}
  });
</script>

<main>
<!-- main parted in sections, for scroll and styling -->
	<section class="charactersection">
		<h1>Choose your character</h1>

			<ul>
				<li><img class="harry" src="images/harry.png" alt="harry"></li>
				<li><img class="hermelien" src="images/hermelien.png" alt="hermelien"></li>
				<li><img class="ron" src="images/ron.png" alt="ron"></li>
				<li><img class="neville" src="images/neville.png" alt="neville"></li>
				<li><img class="draco" src="images/draco.png" alt="draco"></li>
				<li><img class="sirius" src="images/sirius.png" alt="sirius"></li>
				<li><img class="snape" src="images/sneep.png" alt="snape"></li>
			</ul>

			<div class="harryClick"></div>

			<button>watch the stats!</button>
	</section>

	<section class="harrysection">
		<h1>harry</h1>
		<img src="../images/harrypotterstaand.png" alt="">

<!-- condition rendering for certain data to pop up -->
		{#if selectedCharacterHarryData}
      <ul class="datalist">
        <li>Name: {selectedCharacterHarryData.name}</li>
		<li>Hair color: {selectedCharacterHarryData.hairColour}</li>
        <li>House: {selectedCharacterHarryData.house}</li>
		<li>Hogwarts student: {selectedCharacterHarryData.hogwartsStudent}</li>
        <li>Species: {selectedCharacterHarryData.species}</li>
        <li>Ancestry: {selectedCharacterHarryData.ancestry}</li>
        <li>alive: {selectedCharacterHarryData.alive}</li>
        <li>Patronus: {selectedCharacterHarryData.patronus}</li>
      </ul>
    	{/if}
	</section>

	<section class="hermionesection">
		<h1>hermione</h1>
		<img src="../images/hermelienstaand.png" alt="">

<!-- condition rendering for certain data to pop up -->
		{#if selectedCharacterHermioneData}
    <ul class="datalist">
      <li>Name: {selectedCharacterHermioneData.name}</li>
	  <li>Hair color: {selectedCharacterHermioneData.hairColour}</li>
      <li>House: {selectedCharacterHermioneData.house}</li>
	  <li>Hogwarts student: {selectedCharacterHermioneData.hogwartsStudent}</li>
      <li>Species: {selectedCharacterHermioneData.species}</li>
      <li>Ancestry: {selectedCharacterHermioneData.ancestry}</li>
      <li>Alive: {selectedCharacterHermioneData.alive}</li>
      <li>Patronus: {selectedCharacterHermioneData.patronus}</li>
    </ul>
  	{/if}
	</section>

	<section class="ronsection">
		<h1>ron</h1>
		<img src="../images/ronstaand.png" alt="">

<!-- condition rendering for certain data to pop up -->
		{#if selectedCharacterRonData}
		<ul class="datalist">
		  <li>Name: {selectedCharacterRonData.name}</li>
		  <li>Hair color: {selectedCharacterRonData.hairColour}</li>
		  <li>House: {selectedCharacterRonData.house}</li>
		  <li>Hogwarts student: {selectedCharacterRonData.hogwartsStudent}</li>
		  <li>Species: {selectedCharacterRonData.species}</li>
		  <li>Ancestry: {selectedCharacterRonData.ancestry}</li>
		  <li>Alive: {selectedCharacterRonData.alive}</li>
		  <li>Patronus: {selectedCharacterRonData.patronus}</li>
		</ul>
	  	{/if}
	</section>

	<section class="nevillesection">
		<h1>neville</h1>
		<img src="../images/nevillestaand.png" alt="">

<!-- condition rendering for certain data to pop up -->
		{#if selectedCharacterNevilleData}
		<ul class="datalist">
		  <li>Name: {selectedCharacterNevilleData.name}</li>
		  <li>Hair color: {selectedCharacterNevilleData.hairColour}</li>
		  <li>House: {selectedCharacterNevilleData.house}</li>
		  <li>Hogwarts student: {selectedCharacterNevilleData.hogwartsStudent}</li>
		  <li>Species: {selectedCharacterNevilleData.species}</li>
		  <li>Ancestry: {selectedCharacterNevilleData.ancestry}</li>
		  <li>Alive: {selectedCharacterNevilleData.alive}</li>
		  <li>Patronus: {selectedCharacterNevilleData.patronus}</li>
		</ul>
	  	{/if}
	</section>

	<section class="dracosection">
		<h1>draco</h1>
		<img src="../images/dracostaand.png" alt="">

<!-- condition rendering for certain data to pop up -->
		{#if selectedCharacterDracoData}
		<ul class="datalist">
		  <li>Name: {selectedCharacterDracoData.name}</li>
		  <li>Hair color: {selectedCharacterDracoData.hairColour}</li>
		  <li>House: {selectedCharacterDracoData.house}</li>
		  <li>Hogwarts student: {selectedCharacterDracoData.hogwartsStudent}</li>
		  <li>Species: {selectedCharacterDracoData.species}</li>
		  <li>Ancestry: {selectedCharacterDracoData.ancestry}</li>
		  <li>Alive: {selectedCharacterDracoData.alive}</li>
		  <li>Patronus: {selectedCharacterDracoData.patronus}</li>
		</ul>
	  	{/if}
	</section>

	<section class="siriussection">
		<h1>sirius</h1>
		<img src="../images/siriusstaand.png" alt="">

<!-- condition rendering for certain data to pop up -->
		{#if selectedCharacterSiriusData}
		<ul class="datalist">
		  <li>Name: {selectedCharacterSiriusData.name}</li>
		  <li>Hair color: {selectedCharacterSiriusData.hairColour}</li>
		  <li>House: {selectedCharacterSiriusData.house}</li>
		  <li>Hogwarts student: {selectedCharacterSiriusData.hogwartsStudent}</li>
		  <li>Species: {selectedCharacterSiriusData.species}</li>
		  <li>Ancestry: {selectedCharacterSiriusData.ancestry}</li>
		  <li>Alive: {selectedCharacterSiriusData.alive}</li>
		  <li>Patronus: {selectedCharacterSiriusData.patronus}</li>
		</ul>
	  	{/if}
	</section>

	<section class="snapesection">
		<h1>snape</h1>
		<img src="../images/snapestaand.png" alt="">

<!-- condition rendering for certain data to pop up -->
		{#if selectedCharacterSnapeData}
		<ul class="datalist">
		  <li>Name: {selectedCharacterSnapeData.name}</li>
		  <li>Hair color: {selectedCharacterSnapeData.hairColour}</li>
		  <li>House: {selectedCharacterSnapeData.house}</li>
		  <li>Hogwarts student: {selectedCharacterSnapeData.hogwartsStudent}</li>
		  <li>Species: {selectedCharacterSnapeData.species}</li>
		  <li>Ancestry: {selectedCharacterSnapeData.ancestry}</li>
		  <li>Alive: {selectedCharacterSnapeData.alive}</li>
		  <li>Patronus: {selectedCharacterSnapeData.patronus}</li>
		</ul>
	  	{/if}
	</section>

	<section class="graphicssection">
		<h1>data</h1>	

<!-- loading in my components -->
		<Barchart />
		<Dotplot />

		<button class="goBackButton">go back to characters</button>

	</section>
</main>