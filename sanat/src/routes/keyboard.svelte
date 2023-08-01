<script lang="ts">
    import Key from "./key.svelte";
    import { wrong, right, place, empty } from "./util";

    const rows = [
        ['q', 'w', 'e', 'r', 't', 'y', 'u', 'i', 'o', 'p', 'å', "<"],
        ['a', 's', 'd', 'f', 'g', 'h', 'j', 'k', 'l', 'ö', 'ä'],
        ['z', 'x', 'c', 'v', 'b', 'n', 'm', "_"]
    ];

    function remove_letter(letter: string) {
        input = input.substring(0, Math.max(0, input.length - 1));
        callback(input, false)
    }

    function add_letter(letter: string) {
        if (input.length < 5) {
            input = input + letter;
            callback(input, false)
        }
    }

    function enter(letter: string) {
        if (input.length >= 5) {
            callback(input, true);
            input = "";
        }
    }

    export let callback = (word: string, ready: boolean) => {};

    let input = "";

    export let correct = new Set<string>();
    export let incorrect = new Set<string>();
    export let wrongplace = new Set<string>();
</script>

<div class="container text-secondary">
    {#each rows as row}
    <div class="row justify-content-center">
        {#each row as key}
            {#if key === '<'}
                <Key key={"\u232B"} callback={remove_letter} color={empty}/>
            {:else if key === '_'}
                <Key key={"\u23CE"} callback={enter} color={empty}/>
            {:else}
                <Key key={key} callback={add_letter} color={correct.has(key) ? right : (wrongplace.has(key) ? wrong : (incorrect.has(key) ? place : empty))}/>
            {/if}
        {/each}
    </div>
    {/each}
</div>