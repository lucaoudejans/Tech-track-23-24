<script>
    import { onMount } from 'svelte';

    onMount(async () => {
        // JavaScript om klikgebeurtenissen aan de afbeeldingen toe te voegen
    var harry = document.querySelector('.harry');
    var harryClick = document.querySelector('.harryClick');

    harry.addEventListener('click', function(event) {
      if (event.target.tagName === 'IMG') {
        toonAfbeelding(event.target.src);
      }
    });

    // JavaScript-functie om de afbeelding weer te geven
    function toonAfbeelding(afbeeldingBron) {
      // Verander de HTML van het element om de geselecteerde afbeelding weer te geven
      harryClick.innerHTML = '<img src="../images/harrystaand.png"' + afbeeldingBron + '" alt="Weergegeven afbeelding">';
    }
    });	
</script>

