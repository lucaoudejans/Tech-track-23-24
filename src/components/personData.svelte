<script>
		import { onMount } from 'svelte';

		onMount(async () => {
				// Maak een fetch-aanroep naar de opgegeven URL
		fetch('https://hp-api.onrender.com/api/characters')
		.then(response => {
			// Controleer of het verzoek succesvol was (statuscode 200-299)
			if (!response.ok) {
			throw new Error('Network response was not ok');
			}
			// Converteer de respons naar JSON-formaat
			return response.json();
		})
		.then(data => {
			// Lijst met gewenste personages
			const desiredCharacters = ['Harry Potter', 'Hermione Granger', 'Ron Weasley', 'Draco Malfoy', 'Neville Longbottom', 'Severus Snape', 'Sirius Black'];

			// Filter de gegevens op basis van de lijst met gewenste personages
			const filteredCharacters = data.filter(character => desiredCharacters.includes(character.name));

			// Verwerk de gefilterde gegevens
			console.log(filteredCharacters);
		})
		.catch(error => {
			// Vang eventuele fouten op tijdens het fetchen van gegevens
			console.error('There was a problem with the fetch operation:', error);
		});
		});
		
</script>

