<script>
    export let spells;
</script>

{#each spells as spell}
    <tr>
        <td class="border px-4 py-2">{spell.name}</td>
        <td class="border px-4 py-2">{spell.level}</td>
        <td class="border px-4 py-2">{spell.is_ritual}</td>
        <td class="border px-4 py-2">{spell.casting_time}</td>
        <td class="border px-4 py-2">{spell.range}</td>
        <td class="border px-4 py-2">
            {spell.spell_lists.map((spellList) => spellList.name).join(', ')}
        </td>
    </tr>
{/each}
