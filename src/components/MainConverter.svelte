<script lang="ts">
    import ConverterButton from "./ConverterButton.svelte";
    let apiFrom: string[] = [];
    let apiTo: string[] = [];

    fetch(`https://open.er-api.com/v6/latest/RUB`)
        .then((res) => res.json())
        .then((data) => {
            for (let i in data.rates) {
                apiFrom[apiFrom.length] = i;
                apiTo[apiTo.length] = i;
            }
        });

    type API = {
        moneyFrom: number;
        moneyTo: number;
        curFrom: string;
        curTo: string;
    };

    let api: API = {
        moneyFrom: 0,
        moneyTo: 0,
        curFrom: "",
        curTo: "",
    };
    let result: string = "";
    function submit() {
        fetch(`https://open.er-api.com/v6/latest/${api.curFrom}`)
            .then((res) => res.json())
            .then((data) => {
                api.moneyTo = api.moneyFrom;
                for (let i in data.rates) {
                    if (i === api.curTo) {
                        api.moneyTo *= data.rates[i];
                        console.log(data.rates[i]);
                        result = `${api.moneyFrom} ${api.curFrom} = ${api.moneyTo} ${api.curTo}`;
                        console.log(result);
                        break;
                    }
                }
            });
    }
</script>

<main>
    <div class="container" id="converter-main">
        <form id="apiForm" on:submit|preventDefault={submit}>
            <div class="flexBox">
                <p>Amount</p>
                <input
                    type="number"
                    id="apiAmount"
                    bind:value={api.moneyFrom}
                />
            </div>
            <div class="flexBox">
                <p>From</p>
                <select id="apiFrom" bind:value={api.curFrom}>
                    {#each apiFrom as data}
                        <option value={data}>{data}</option>
                    {/each}
                </select>
            </div>
            <div class="flexBox">
                <p>To</p>
                <select id="apiTo" autocomplete="off" bind:value={api.curTo}>
                    {#each apiFrom as data}
                        <option value={data}>{data}</option>
                    {/each}
                </select>
            </div>
            <div id="apiButton">
                <ConverterButton
                    on:message={submit}
                    curFrom={api.curFrom}
                    curTo={api.curTo}
                />
            </div>

            <div class="flexBox" id="apiResult">
                <p>{result}</p>
            </div>
        </form>
    </div>
</main>

<style>
    #converter-main {
        background-color: #a1c3ff;
        width: 40%;
        max-width: 700px;
        margin-bottom: 10px;
        border-radius: 10px;
        border-width: 5px;
        border-color: cadetblue;
        border-style: solid;
    }
    #apiForm {
        display: flex;
        justify-content: center;
        flex-wrap: wrap;
    }
    .flexBox {
        display: flex;
        flex-direction: column;
        align-items: start;
        align-content: center;
    }
    .flexBox p {
        margin: 0;
        padding-top: 5px;
        padding-left: 12px;
        color: black;
    }
    .flexBox input {
        margin: 10px;
        padding: 5px;
        border-radius: 5px;
        border-color: cadetblue;
        background-color: azure;
    }
    .flexBox select {
        margin: 10px;
        padding: 5px;
        border-radius: 5px;
        border-color: cadetblue;
        background-color: azure;
    }
    #apiButton {
        width: 80%;
        margin: 10px;
    }
</style>
