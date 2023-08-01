<script lang="ts">
    import Words from "./words.svelte";
    import { word_list } from "./util";
    import Keyboard from "./keyboard.svelte";

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
        console.log(correct_letters);
        console.log(wrongplace_letters);
        console.log(incorrect_letters);
        console.log("========");
    }

    function add_word(word: string, ready: boolean) {
        if (i >= 6) {
            return;
        }
        words[i] = word + (ready ? " " : "");
        if (ready && words[i].length === 6) {
            console.log('"' + words[i] + '"');
            i++;
            if (i >= 6) {
                message = `Sana oli "${correct}"`
            }
            get_letters();
        }
        words = words;
    }

    let i = 0;

    let correct = word_list[Math.floor(Math.random() * word_list.length)];

    let message = "";

    let correct_letters = new Set<string>();
    let incorrect_letters = new Set<string>();
    let wrongplace_letters = new Set<string>();
 
    export let words = [
        "", "", "", "", "", ""
    ]
</script>

<div class="container">
    <h1 class="text-center">SANAT</h1>
    <Words words={words} correct={correct}/>
    <p class="text-center">{message}</p>
</div>
<Keyboard callback={add_word} correct={correct_letters} incorrect={incorrect_letters} wrongplace={wrongplace_letters}/>
