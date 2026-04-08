<script>
    import { onMount } from "svelte";
    import thousandsFormat from "./thousandsFormat";
    
    export let label;
    export let amount;
    export let timestamp;
    let custom = false;
    const date = new Date(timestamp*1000);
    const months = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"];

    // console.log(label)
    if(label == null) {
        // console.log("custom")
        custom = true;
        onMount(() => {
            document.getElementById("icon"+timestamp).remove()
        })
        if(amount == 0) {
            label = "Reset";
        } else {
            label = "Coupon";
        }
    }
</script>

<div class="flex flex-col w-full">
    <div class="flex flex-row items-center gap-2 p-2 justify-between w-full">
        <i id="icon{timestamp}" class="fa-solid fa-money-bill-transfer"></i>
        <div class="flex flex-row items-center justify-between w-full">
            <div class="flex flex-col">
                <span class="font-bold leading-5">{label}</span>
                <span class="{custom ? 'text-xs leading-5' : 'hidden'}">{date.getDate()} {months[date.getMonth()]} {date.getFullYear()}</span>
            </div>
            <span class="{custom ? 'font-bold '+(amount == 0 ? 'text-red-800' : 'text-green-800') : ''}">{custom ? '' : '-'}Rp{thousandsFormat(amount)}</span>
        </div>
    </div>
    <div class="w-full bg-black/25" style="height: 1px;"></div>
</div>