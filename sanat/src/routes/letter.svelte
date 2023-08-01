<script>
    import { right, wrong, place } from './util';

    export let letter = ' ';
    export let correct = 0;
</script>

{#key letter}{#key correct}
<div class="col border text-center fs-4 pt-2 { correct === wrong ? "bg-secondary" : "" } { correct === place ? "bg-warning" : "" } { correct === right ? "bg-success" : "" }" style="max-width: 50px; max-height: 50px; min-width: 50px; min-height: 50px">
    <span>{letter}</span>
</div>
{/key}{/key}