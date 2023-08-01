<script>
    import Row from "./row.svelte";

    export let correct = "";
    export let words = ["", "", "", "", "", ""];
</script>

<div class="d-flex justify-content-center">
    <div class="container" style="max-width: 255px">
        <Row word={words[0]} correct={correct}/>   
        <Row word={words[1]} correct={correct}/>
        <Row word={words[2]} correct={correct}/>
        <Row word={words[3]} correct={correct}/>
        <Row word={words[4]} correct={correct}/>
        <Row word={words[5]} correct={correct}/>
    </div>
</div>