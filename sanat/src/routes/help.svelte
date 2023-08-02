<script lang="ts">
    export let close_fn = () => {};
</script>

<div class="shadow w-50 container bg-white position-absolute start-50 top-50 translate-middle" style="min-width: 250px">
    <div class="position-relative m-2"><button class="btn position-absolute end-0 top-0 rounded-circle shadow" on:click={close_fn}>X</button></div>
    <div class="text-center">
        <h2>Ohje</h2>
        <p>Pelin tavoite on arvata kuudella arvauksella viisikirjaiminen sana. Arvattujen sanojen kirjaimet antavat vihjeitä siitä mikä oikea sana on.</p>
        <p>Kirjoita sana näppäimistöllä ja paina <strong class="fs-4">{"\u23CE"}</strong>-näppäintä arvataksesi sanaa. Sanassa olevat kirjaimet muuttavat
            väriä ja voit arvata uutta sanaa. <strong>{"\u232B"}</strong>-näppäimellä voit peruutta kirjoitettuja merkkejä.</p>
        <p>Kirjainten värit merkitsevät seuraavaa:</p>
        <div class="text-start">
            <p><span class="bg-success p-1">A</span> kirjain on oikein, eli oikeassa sanassa on tämä sama kirjain samassa kohdassa sanaa.</p>
            <p><span class="bg-warning p-1">K</span> oikeassa sanassa on kyseinen kirjain, mutta se on jossain toisessa kohdassa kuin arvasit.</p>
            <p><span class="bg-secondary p-1">S</span> kirjain on väärin ja se ei siis esiinny oikeassa sanassa.</p>
        </div>
    </div>
</div>