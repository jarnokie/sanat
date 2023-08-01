<script lang="ts">
    import { onMount } from "svelte";
    import Letter from "./letter.svelte";
    import { right, wrong, place, empty } from './util';
    let colors = [0, 0, 0, 0, 0];

    function color_for(i: number, w: string, correct: string) {
        if(w.charAt(i) === correct.charAt(i)) {
            return right;
        }
        const c = w.charAt(i);
        for (let j = 0; j < 5; j++) {
            if (correct.charAt(j) == c && correct.charAt(j) != w.charAt(j)) {
                return place;
            }
        }
        return wrong;
    }

    function calculate_colors(w: string) {
        let new_colors = [0, 0, 0, 0, 0]
        if (w.length > 5) {
            for (let i = 0; i < 5; i++) {
                new_colors[i] = color_for(i, w, correct);
            }
        }
        return new_colors;
    }

    $: {
        colors = calculate_colors(word);
    }

    export let correct = "";

    export let word = "";

    onMount(async () => colors = calculate_colors(word));
</script>

<div class="row">
    <Letter letter={word.charAt(0).toUpperCase()} correct={colors[0]}/>
    <Letter letter={word.charAt(1).toUpperCase()} correct={colors[1]}/>
    <Letter letter={word.charAt(2).toUpperCase()} correct={colors[2]}/>
    <Letter letter={word.charAt(3).toUpperCase()} correct={colors[3]}/>
    <Letter letter={word.charAt(4).toUpperCase()} correct={colors[4]}/>
</div>