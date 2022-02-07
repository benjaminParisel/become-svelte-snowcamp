<script>
    import { poids, taille, imc } from './stores'
    import { fly, fade } from 'svelte/transition';

    $: thin = $imc < 18
    $: bold = $imc > 35
</script>

<svelte:head>
    <title>Votre IMC : {$imc}</title>
</svelte:head>

<p class:thin class:bold>
    Votre IMC ({$poids}/{$taille}<sup>2</sup>) est de {$imc}
</p>
{#if thin}
    <p class="souspoids" in:fly="{{ y: 200, duration: 2000 }}" out:fade>
        Vous êtes maigre
    </p>
{:else if bold}
    <p class="surpoids" in:fly="{{ y: 200, duration: 2000 }}" out:fade>
        Vous êtes en surpoids
    </p>
{:else}
    <p class="normal" in:fly="{{ y: 200, duration: 2000 }}" out:fade>
        Vous êtes svelte !
    </p>
{/if}