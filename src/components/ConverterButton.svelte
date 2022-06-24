<script lang="ts">
    import { createEventDispatcher } from "svelte";

    export let curFrom:string;
    export let curTo:string;

    $: falseInput = (!curFrom || !curTo);
    const dispatch = createEventDispatcher();
    function send() {
        dispatch('message', {})
    }
</script>

<main>
    
    <button id="apiButton" on:click={send} disabled={falseInput}>Send</button>
</main>

<style>
    #apiButton:disabled{
        cursor:auto;
    }
    #apiButton {
        width: 100%;
        text-decoration: none;
        background-color: azure;
        padding: 10px;
        border:none;
        border-radius: 5px;
        cursor: pointer;
    }
</style>
