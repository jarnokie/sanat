<script lang="ts">
    import Words from "./words.svelte";
    import { word_list } from "./util";
    import Keyboard from "./keyboard.svelte";
    import Help from "./help.svelte";

    function toggle_help() {
        show_help = !show_help;
    }

    function restart() {
        words = ["", "", "", "", "", ""];
        message = "";
        correct_letters = new Set<string>();
        incorrect_letters = new Set<string>();
        wrongplace_letters = new Set<string>();
        correct = word_list[Math.floor(Math.random() * word_list.length)];
        i = 0;
    }

    function get_letters() {
        words.forEach((val, i, arr) => {
            for (let j = 0; j < 5; j++) {
                const c = val.charAt(j);
                if (c === correct.charAt(j)) {
                    correct_letters.add(c);
                } else if (correct.includes(c)) {
                    wrongplace_letters.add(c);
                } else {
                    incorrect_letters.add(c);
                }
            }
        });
        incorrect_letters = incorrect_letters;
        wrongplace_letters = wrongplace_letters;
        correct_letters = correct_letters;
    }

    function add_word(word: string, ready: boolean) {
        if (i >= 6) {
            // Game has ended
            return;
        }
        // Set the current word, append space to complete the word if it is commited.
        words[i] = word + (ready ? " " : "");
        if (ready && words[i].length === 6) {
            if (!word_list.includes(word)) {
                words[i] = "";
                words = words;
                message = `${word} ei ole sana!`
                return;
            }

            if (word === correct) {
                // End the game if correct word was quessed.
                i = 6;
            }
            i++;
            if (i >= 6) {
                message = `Sana oli "${correct}"`
            }
            // Set the keyboard colors
            get_letters();
        }
        // Trigger update to the Words element.
        words = words;
    }

    let i = 0;

    let correct = word_list[Math.floor(Math.random() * word_list.length)];

    let message = "";

    let show_help = false;

    let correct_letters = new Set<string>();
    let incorrect_letters = new Set<string>();
    let wrongplace_letters = new Set<string>();
 
    export let words = [
        "", "", "", "", "", ""
    ]
</script>

<svelte:head>
    <title>SANAT</title>
</svelte:head>

<div class="container text-center">
    <h1>SANAT</h1>
    <Words words={words} correct={correct}/>
    <p>{message} {#if i >= 6}<button class="btn btn-primary mt-1" on:click={restart}>Uudestaan?</button>{/if}</p>
</div>
<Keyboard callback={add_word} correct={correct_letters} incorrect={incorrect_letters} wrongplace={wrongplace_letters}/>

{#if show_help}<Help close_fn={toggle_help}/>{/if}
<button class="btn shadow position-absolute text-center top-0 end-0 m-1 m-sm-5 rounded-circle" style="width: 75px; height: 75px;"
        on:click={toggle_help}>
    <strong class="fs-4">?</strong>
</button>
