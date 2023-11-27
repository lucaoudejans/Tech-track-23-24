<!-- <script>

    import { onMount } from 'svelte';
    onMount(async () => {
        // JavaScript om klikgebeurtenissen aan de afbeeldingen toe te voegen
        const characterList = document.querySelector('ul');
        const characterClick = document.querySelector('.harryClick');
        let currentStaandAfbeelding = null;

        // Mapping van karakternamen naar bijbehorende staande afbeeldingen
        const staandeAfbeeldingen = {
        'Harry Potter': 'harrypotterstaand.png',
        'Hermione Granger': 'hermelienstaand.png',
        'Ron Weasley': 'ronstaand.png',
        'Neville Longbottom': 'nevillestaand.png',
        'Draco Malfoy': 'dracostaand.png',
        'Sirius Black': 'siriusstaand.png',
        'Severus Snape': 'snapestaand.png',
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
    <ul>
        <li><img class="Harry Potter" src="images/harry.png" alt="harry"></li>
        <li><img class="Hermione Granger" src="images/hermelien.png" alt="hermelien"></li>
        <li><img class="Ron Weasley" src="images/ron.png" alt="ron"></li>
        <li><img class="Neville Longbottom" src="images/neville.png" alt="neville"></li>
        <li><img class="Draco Malfoy" src="images/draco.png" alt="draco"></li>
        <li><img class="Sirius Black" src="images/sirius.png" alt="sirius"></li>
        <li><img class="Severus Snape" src="images/sneep.png" alt="snape"></li>
    </ul>

    <div class="harryClick"></div>
</main>

<style>
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
 -->
