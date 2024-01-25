<!-- This project is made by Luca Oudejans in association with ChatGPT, resources and the teachers from tech track. 
The resources can be found in my Wiki! -->
<!-- Linking stylesheet -->
<svelte:head>
	<link rel="stylesheet" href="style.css" />
</svelte:head>

<!-- importing onmount and components -->
<script>
import { onMount } from 'svelte';
import Barchart from '../components/barchart.svelte';
import Dotplot from '../components/dotplot.svelte';

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

// to check if the specific characters have been filterede
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

		{#if selectedCharacterHarryData}
    		<ul class="datalist">
      			{#each Object.entries(selectedCharacterHarryData) as [key, value]}
	  				{#if key === 'name' || key === 'house' || key === 'hogwartsStudent' || key === 'hairColour' || key === 'species' || key === 'ancestry' || key === 'alive' || key === 'patronus'} 
	  				<li>{key}: {value}</li>
					{/if}
      			{/each}
    		</ul>
  		{/if}
	</section>

	<section class="hermionesection">
		<h1>hermione</h1>
		<img src="../images/hermelienstaand.png" alt="">

		{#if selectedCharacterHermioneData}
    		<ul class="datalist">
      			{#each Object.entries(selectedCharacterHermioneData) as [key, value]}
	  				{#if key === 'name' || key === 'house' || key === 'hogwartsStudent' || key === 'hairColour' || key === 'species' || key === 'ancestry' || key === 'alive' || key === 'patronus'} 
	  				<li>{key}: {value}</li>
					{/if}
      			{/each}
    		</ul>
  		{/if}
	</section>

	<section class="ronsection">
		<h1>ron</h1>
		<img src="../images/ronstaand.png" alt="">

		{#if selectedCharacterRonData}
    		<ul class="datalist">
      			{#each Object.entries(selectedCharacterRonData) as [key, value]}
	  				{#if key === 'name' || key === 'house' || key === 'hogwartsStudent' || key === 'hairColour' || key === 'species' || key === 'ancestry' || key === 'alive' || key === 'patronus'} 
	  				<li>{key}: {value}</li>
					{/if}
      			{/each}
    		</ul>
  		{/if}
	</section>

	<section class="nevillesection">
		<h1>neville</h1>
		<img src="../images/nevillestaand.png" alt="">

		{#if selectedCharacterNevilleData}
    		<ul class="datalist">
      			{#each Object.entries(selectedCharacterNevilleData) as [key, value]}
	  				{#if key === 'name' || key === 'house' || key === 'hogwartsStudent' || key === 'hairColour' || key === 'species' || key === 'ancestry' || key === 'alive' || key === 'patronus'} 
	  				<li>{key}: {value}</li>
					{/if}
      			{/each}
    		</ul>
  		{/if}
	</section>

	<section class="dracosection">
		<h1>draco</h1>
		<img src="../images/dracostaand.png" alt="">

		{#if selectedCharacterDracoData}
    		<ul class="datalist">
      			{#each Object.entries(selectedCharacterDracoData) as [key, value]}
	  				{#if key === 'name' || key === 'house' || key === 'hogwartsStudent' || key === 'hairColour' || key === 'species' || key === 'ancestry' || key === 'alive' || key === 'patronus'} 
	  				<li>{key}: {value}</li>
					{/if}
      			{/each}
    		</ul>
  		{/if}
	</section>

	<section class="siriussection">
		<h1>sirius</h1>
		<img src="../images/siriusstaand.png" alt="">

		{#if selectedCharacterSiriusData}
    		<ul class="datalist">
      			{#each Object.entries(selectedCharacterSiriusData) as [key, value]}
	  				{#if key === 'name' || key === 'house' || key === 'hogwartsStudent' || key === 'hairColour' || key === 'species' || key === 'ancestry' || key === 'alive' || key === 'patronus'} 
	  				<li>{key}: {value}</li>
					{/if}
      			{/each}
    		</ul>
  		{/if}
	</section>

	<section class="snapesection">
		<h1>snape</h1>
		<img src="../images/snapestaand.png" alt="">

		{#if selectedCharacterSnapeData}
    		<ul class="datalist">
      			{#each Object.entries(selectedCharacterSnapeData) as [key, value]}
	  				{#if key === 'name' || key === 'house' || key === 'hogwartsStudent' || key === 'hairColour' || key === 'species' || key === 'ancestry' || key === 'alive' || key === 'patronus'} 
	  				<li>{key}: {value}</li>
					{/if}
      			{/each}
    		</ul>
  		{/if}
	</section>

	<section class="graphicssection">
		<h1>data</h1>
		<p class="datateksts">Now that you have met all the characters, we can point out certain things. The first chart is a barchart with 
		data about who is a student and who is not, the peculiar thing is that all the students are still alive and the 
		'not students' are deceased.
		The second chart is about their hair color and ancestory. The funny thing about this chart is that you can see
		with one look that 'pure blood' has all the hair colors unlike the other ancestories. Hover over the charts to find out more!	
		</p>	

<!-- loading in my components -->
		<Barchart />
		<Dotplot />

		<button class="goBackButton">go back to characters</button>

	</section>
</main>