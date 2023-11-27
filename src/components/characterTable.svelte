<script>
  export let characters = [];
</script>

<main>
    <table>
    <thead>
        <tr>
        <th>Name</th>
        <th>House</th>
        <!-- Voeg hier andere gewenste kolommen toe -->
        </tr>
    </thead>
    <tbody>
        {#each characters as character (character.id)}
        <tr>
            <td>{character.name}</td>
            <td>{character.house}</td>
            <!-- Voeg hier andere gewenste kolommen toe -->
        </tr>
        {/each}
    </tbody>
    </table>
</main>

  