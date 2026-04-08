<script>
	import '../../app.css';
    import { getBalance, getMerchantList, getHistory } from '$lib/user.svelte';
    import { get, writable } from 'svelte/store';
    import thousandsFormat from '$lib/thousandsFormat';

    const merchant = writable(undefined);
    const balance = writable(undefined);
    const history = writable([]);
    const merchant_list = writable([]);
    getMerchantList().then((list) => {
        console.log(list)
        merchant_list.set(Object.keys(list))
    })

    const check_data = writable(false);

</script>

<!-- svelte-ignore a11y_no_static_element_interactions -->
<div class="h-dvh w-dvw flex flex-col items-center justify-center gap-4 px-8">

    {#if $check_data == true}
        <h1 class="font-bold text-center" style="font-family: 'Arimo';">{$merchant}</h1>
        <span>Total Revenue: Rp{thousandsFormat($balance)}</span>
        <div class="flex flex-col overflow-scroll max-h-1/2 w-full m-0 px-2 items-center">
            {#each $history as item}
            
            <span class="font-bold text-green-800">+Rp{thousandsFormat(item.amount)} from {item.user_email.split("@")[0]}</span>
            <span class="mb-2">{new Date(item.timestamp*1000).toLocaleDateString("ID")} {new Date(item.timestamp*1000).toLocaleTimeString("US")}</span>

            {/each}
        </div>
        <!-- svelte-ignore a11y_click_events_have_key_events -->
        <div onclick={() => {
            getBalance($merchant).then((response) => {
                console.log($merchant)
                console.log(response)
                balance.set(response)
                getHistory($merchant).then((response) => {
                    history.set(response)
                    check_data.set(true)
                })
            })
        }} class="flex justify-center w-fit py-2 px-4 rounded-full drop-shadow-sm drop-shadow-aztec-gold bg-maize group select-none"><span class="group-active:opacity-50 duration-200">Refresh Data</span></div>
        <!-- svelte-ignore a11y_click_events_have_key_events -->
        <i onclick={() => {check_data.set(false)}} class="opacity-50 active:opacity-25 active:underline duration-200 absolute bottom-10 select-none">exit</i>
    {:else}
        <h1>MERCHANT DASHBOARD</h1>
        <select id="merchant_select" onchange={() => {merchant.set(document.getElementById("merchant_select").value);}} class="py-2 px-4 rounded-full drop-shadow-sm drop-shadow-aztec-gold bg-maize text-center">
            <option disabled selected>Select Merchant</option>
            {#each $merchant_list as merchant_name}
                <option value="{merchant_name}">{merchant_name}</option>
            {/each}
            
        </select>
        <!-- svelte-ignore a11y_click_events_have_key_events -->
        <div onclick={() => {
            getBalance($merchant).then((response) => {
                console.log($merchant)
                balance.set(response)
                getHistory($merchant).then((response) => {
                    history.set(response)
                    check_data.set(true)
                })
            })
        }} class="flex justify-center w-fit py-2 px-4 rounded-full drop-shadow-sm drop-shadow-aztec-gold bg-maize group select-none"><span class="group-active:opacity-50 duration-200">Check <i>{$merchant}</i> Data</span></div>
    {/if}

</div>