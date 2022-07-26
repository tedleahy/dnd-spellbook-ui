<script>
    import TableHeader from "../../components/tables/TableHeader.svelte";
    import SpellRows from "./components/SpellRows.svelte";

    async function fetchSpells() {
        const res = await fetch(
            'http://localhost:5000/spells',
            {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                    'Accept': 'application/json',
                },
            }
        );

        if (!res.ok) {
            console.error('Error fetching spells: ' + res.status, res.body);
        } else {
            const spells = await res.json();
            return spells;
        }
    }

    const displayCols = ['Name', 'Level', 'Ritual?', 'Casting Time', 'Range', 'Spell Lists'];
</script>

<table class="table-auto shadow-lg bg-white">
    <tr>
        {#each displayCols as colName}
            <TableHeader text={colName} />
        {/each}
    </tr>

    {#await fetchSpells()}
        <p>Loading spells...</p>
    {:then spells} 
        <SpellRows spells={spells} />
    {:catch error}
        <p>Error fetching spells:</p>
        <p>{error}</p>
    {/await}
</table>
