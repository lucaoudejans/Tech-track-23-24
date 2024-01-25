<!-- This project is made by Luca Oudejans in association with ChatGPT, resources and the teachers from tech track. 
The resources can be found in my Wiki! -->
<!-- Linking stylesheet -->
<svelte:head>
	<link rel="stylesheet" href="style.css" />
</svelte:head>

<!-- importing onmount and components -->
<script>
import { onMount } from 'svelte';
import Barchart from '../barchart.svelte';
import Dotplot from '../components/dotplot.svelte';


  let characterData = {};


  onMount(async () => {
  try {
    const desiredCharacters = ['Harry Potter', 'Hermione Granger', 'Ron Weasley', 'Draco Malfoy', 'Neville Longbottom', 'Severus Snape', 'Sirius Black'];

    const response = await fetch('https://hp-api.onrender.com/api/characters');
    const data = await response.json();

    const filteredCharacters = data.filter(character => desiredCharacters.includes(character.name));

    filteredCharacters.forEach(character => {
      characterData[character.name.toLowerCase()] = character;
    });

    console.log('Gefilterde karakters:', filteredCharacters);
    console.log('Geselecteerde karakters:', characterData);
  } catch (error) {
    console.error('Er was een probleem met de fetch-operatie:', error);
  }
});

function scrollToSection(targetClass) {
  const targetSection = document.querySelector(`.${targetClass}`);

  if (targetSection) {
    targetSection.scrollIntoView({ behavior: 'smooth' });
  }
}

function handleCharacterClick(event) {
  const target = event.target;
  const characterSection = target.dataset.characterSection;

  if (characterSection) {
    console.log('Clicked section:', characterSection);
    scrollToSection(`${characterSection}section`);
  }
}

function handleButtonClick() {
  scrollToSection('graphicssection');
}

function handleGoBackButtonClick() {
  scrollToSection('charactersection');
}

$: characterImages = [
  { name: 'harry_potter' },
  { name: 'hermione_granger' },
  { name: 'ron_weasley' },
  { name: 'draco_malfoy' },
  { name: 'severus_snape' },
  { name: 'neville_longbottom' },
  { name: 'sirius_black' },
];
</script>

<main>
  <section class="charactersection">
    <h1>Choose your character</h1>

    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
    <!-- li met hp karakters -->
    <ul on:click={handleCharacterClick} class="character-images">
      {#each characterImages as { name }}
        <li><img src={`../images/${name}.png`} alt="" data-character-section={name.toLowerCase()}></li>
      {/each}
    </ul>

    <div class="harryClick"></div>

    <button on:click={handleButtonClick}>watch the stats!</button>
  </section>

  {#each Object.keys(characterData) as characterName}
    <section class={`${characterName.toLowerCase().replace(/\s+/g, '_')}section`}>
      <h1>{characterName}</h1>
      <img src={`../images/${characterName.toLowerCase().replace(/\s+/g, '_')}staand.png`} alt="">

      {#if characterData[characterName]}
        <ul class="datalist">
          {#each Object.entries(characterData[characterName]) as [key, value]}
            {#if key === 'name' || key === 'house' || key === 'hogwartsStudent' || key === 'hairColour' || key === 'species' || key === 'ancestry' || key === 'alive' || key === 'patronus'}
              <li>{key}: {value}</li>
            {/if}
          {/each}
        </ul>
      {/if}
    </section>
  {/each}

  <section class="graphicssection">
    <h1>data</h1>
    <p class="datateksts">Now that you have met all the characters, we can point out certain things. The first chart is a barchart with 
      data about who is a student and who is not, the peculiar thing is that all the students are still alive and the 
      'not students' are deceased.
      The second chart is about their hair color and ancestry. The funny thing about this chart is that you can see
      with one look that 'pure blood' has all the hair colors unlike the other ancestories. Hover over the charts to find out more!  
    </p>

    <!-- loading in my components -->
    <Barchart />
    <Dotplot />

    <button on:click={handleGoBackButtonClick} class="goBackButton">go back to characters</button>
  </section>
</main>