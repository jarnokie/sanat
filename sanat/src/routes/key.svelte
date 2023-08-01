<script lang="ts">
    import { right, wrong, place, empty } from "./util";

    export let key = 'a';
    export let callback = (x: string) => {};
    export let color = empty;
</script>

<button class="col-1 border text-light border-secondary p-2 pt-0 pb-1 text-center {color != wrong && color != right && color != place ? "bg-dark" : ""} {color == wrong ? "bg-secondary" : ""} {color == right ? "bg-success" : ""}  {color == place ? "bg-warning" : ""}"
    on:click={callback(key)}>
    <span class="fs-3">{key.toUpperCase()}</span>
</button>