<svelte:head>
	<link rel="stylesheet" href="style.css" />
</svelte:head>

<script>
	import { onMount } from 'svelte';
  import CharacterSelector from '../components/personData.svelte';

  let selectedCharacterData = null;

  onMount(() => {
    const desiredCharacters = ['Harry Potter', 'Hermione Granger', 'Ron Weasley', 'Draco Malfoy', 'Neville Longbottom', 'Severus Snape', 'Sirius Black'];

    fetch('https://hp-api.onrender.com/api/characters')
      .then(response => response.json())
      .then(data => {
        const filteredCharacters = data.filter(character => desiredCharacters.includes(character.name));
        selectedCharacterData = filteredCharacters[0];
      })
      .catch(error => {
        console.error('There was a problem with the fetch operation:', error);
      });
  });

onMount(async () => {
    function scrollToSection(targetClass) {
      const targetSection = document.querySelector(`.${targetClass}`);

      if (targetSection) {
        targetSection.scrollIntoView({ behavior: 'smooth' });
      }
    }

    // Event listener voor Harry
    document.querySelectorAll('.harry').forEach((harryElement) => {
      harryElement.addEventListener('click', () => {
        scrollToSection('harrysection');
      });
    });

    // Event listener voor Hermelien
    document.querySelectorAll('.hermelien').forEach((hermelienElement) => {
      hermelienElement.addEventListener('click', () => {
        scrollToSection('hermionesection');
      });
    });

	    // Event listener voor Ron
		document.querySelectorAll('.ron').forEach((ronElement) => {
      ronElement.addEventListener('click', () => {
        scrollToSection('ronsection');
      });
    });

	    // Event listener voor Neville
		document.querySelectorAll('.neville').forEach((nevilleElement) => {
      nevilleElement.addEventListener('click', () => {
        scrollToSection('nevillesection');
      });
    });

	    // Event listener voor Draco
		document.querySelectorAll('.draco').forEach((dracoElement) => {
      dracoElement.addEventListener('click', () => {
        scrollToSection('dracosection');
      });
    });

	    // Event listener voor Sirius
		document.querySelectorAll('.sirius').forEach((siriusElement) => {
      siriusElement.addEventListener('click', () => {
        scrollToSection('siriussection');
      });
    });

	    // Event listener voor Snape
		document.querySelectorAll('.snape').forEach((snapeElement) => {
      snapeElement.addEventListener('click', () => {
        scrollToSection('snapesection');
      });
    });
  
  });
</script>

<main>
	<section>
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

		{#if selectedCharacterData}
      <ul class="datalist">
        <li>Name: {selectedCharacterData.name}</li>
        <li>House: {selectedCharacterData.house}</li>
        <li>Species: {selectedCharacterData.species}</li>
        <li>Ancestry: {selectedCharacterData.ancestry}</li>
        <li>Date of Birth: {selectedCharacterData.dateOfBirth}</li>
        <li>Patronus: {selectedCharacterData.patronus}</li>
      </ul>
    {/if}
	</section>

	<section class="hermionesection">
		<h1>hermione</h1>
		<img src="../images/hermelienstaand.png" alt="">
	</section>

	<section class="ronsection">
		<h1>ron</h1>
		<img src="../images/ronstaand.png" alt="">
	</section>

	<section class="nevillesection">
		<h1>neville</h1>
		<img src="../images/nevillestaand.png" alt="">
	</section>

	<section class="dracosection">
		<h1>draco</h1>
		<img src="../images/dracostaand.png" alt="">
	</section>

	<section class="siriussection">
		<h1>sirius</h1>
		<img src="../images/siriusstaand.png" alt="">
	</section>

	<section class="snapesection">
		<h1>snape</h1>
		<img src="../images/snapestaand.png" alt="">
	</section>

	<section class="datasection">
		<h1>data</h1>
	</section>
</main>

<style>
	*{
    margin: 0;
    padding: 0;
    color: white;
    font-family: 'Papyrus';
	}

	h1 {
		text-align: center;
		margin-top: 3em;
	}

	ul {
		list-style: none;
		display: flex;
		flex-direction: row;
		justify-content: center;
		padding: 5em;
		cursor: pointer;
		margin-top: 2em;
	}

	img {
		width: 10em;
	}

	button { 
		background-color: white;
		color: blue;
		padding: 0.5em;
		border-radius: 1em;
		cursor: pointer;
		width: 10em;
	}

	section{
		height: 60em; 
		width: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	section:first-of-type{
		background-color: rgb(43, 30, 144);
	}

	section:nth-of-type(2){
		background-color: rgb(156,18,3);
	}

	section:nth-of-type(2) > img{
		width: 60em;
		margin-right: 50em;
		margin-top: -5em;
	}

	section:nth-of-type(3){
		background-color: rgb(125, 15, 3);
	}

	section:nth-of-type(3) > img{
		width: 15em;
		margin-right: 54em;
		margin-top: -5em;
	}

	section:nth-of-type(4){
		background-color: rgb(90, 10, 1);
	}

	section:nth-of-type(4) > img{
		width: 17em;
		margin-right: 50em;
		margin-top: -5em;
	}

	section:nth-of-type(5){
		background-color: rgb(59, 6, 0);
	}

	section:nth-of-type(5) > img{
		width: 12em;
		margin-right: 50em;
		margin-top: -5em;
	}

	section:nth-of-type(6){
		background-color: rgb(3,56,7);
	}

	section:nth-of-type(6) > img{
		width: 18em;
		margin-right: 54em;
		margin-top: -5em;
	}

	section:nth-of-type(7){
		background-color: rgb(156,18,3);
	}

	section:nth-of-type(7) > img{
		width: 20em;
		margin-right: 50em;
		margin-top: -8em;
	}

	section:nth-of-type(8){
		background-color: rgb(3,56,7);
	}

	section:nth-of-type(8) > img{
		width: 50em;
		margin-right: 50em;
		margin-top: -8em;
	}

	section:nth-of-type(9){
		background-color: rgb(56, 3, 43);
	}

	.datalist{
    flex-direction: column;
    margin-top: -25em;
    margin-left: 24em;
    font-size: 1.5em;
    width: 13em;
	background-image: url('../images/perkament.webp');
	background-size: cover;
	gap: 1em;
	cursor: default;
	}

	.datalist > li{
		color: black;
		margin-left: 1em;
		font-family: 'Papyrus';
	}

</style>

<CharacterSelector />