<script>
    let stp_value;
    let stp_e60_value;
    let stp_e40_ss_value;
    let stl_10_value;
    let length;
    let separation;
    let bothChecked = false;
    let bothsides;
    $: length = 7500;
    $: separation = 140;
    $: bothsides = 1;
    $: if ((separation > 29 ) && (length > 999 )) { 
        stp_value = (Math.round(length / separation) * bothsides);
        stp_e40_ss_value = (Math.round(length / separation) * 4 * bothsides);
        stp_e60_value = (Math.round(length / separation) * 2 * bothsides);
        stl_10_value = length;
    } else {
        stp_value = "";
        stp_e40_ss_value = "";
        stp_e60_value = "";
        stl_10_value = "";
    }
    const setblank = () => {
        length = "";
        separation = "";
        bothsides = 1;
        bothChecked = false;
    }
    const setdefault = ()  => {
        length = 7500;
        separation = 140;
        bothChecked = false;
    }
    const handleClick = () => {
        if (!bothChecked) {
            bothsides = 2;
        } else {
            bothsides = 1;
        }
    }
</script>

<svelte:head>
	<title>Calculator</title>
	<meta name="description" content="Your Calculator" />
</svelte:head>

<div class="content">
	<h1 class="text-green-600 pb-3">Conveyer Calculator</h1>
    <div class="pb-4">
        <button on:click="{setdefault}" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">Default</button>
        <button on:click="{setblank}" class="bg-red-600 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">Reset</button>
    </div>
    <form>
        <div class="mb-2 mx-auto pb-3">
            <label for="length" class="text-sm font-medium text-gray-900 block mb-2 dark:text-gray-300">Enter Length</label>
            <input bind:value={length} type="number" id="length" class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
            <label for="Separation" class="pt-4 text-sm font-medium text-gray-900 block mb-2 dark:text-gray-300">Enter Separation</label>
            <input bind:value={separation} type="number" id="separation" class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500 pb-5">
            <div class="align-checkbox pt-5">
            <label for="bscb">Both Sides of Belt:</label>
            <input type=checkbox on:click={handleClick} bind:checked={bothChecked} name="bscb" class="checked:bg-blue-500 pt-5 cb-padding">
        </div>
    </form>
    <hr>
    <div class="container-results mx-auto">
        <div class="align-results">
            <h2 class="text-gray-600 font-bold text-1xl">STP Dual side switch, includes flag:</h2>
            <h2 class="text-gray-600 font-bold text-1xl">{stp_value}</h2>
        </div>
        <div class="align-results">
            <h2 class="text-gray-600 font-bold text-1xl">STP-E60 Compensation spring:</h2>
            <h2 class="text-gray-600 font-bold text-1xl">{stp_e60_value}</h2>
        </div>
        <div class="align-results">
            <h2 class="text-gray-600 font-bold text-1xl">STP-40-SS Rope thimble:</h2>
            <h2 class="text-gray-600 font-bold text-1xl">{stp_e40_ss_value}</h2>
        </div>
        <div class="align-results">
            <h2 class="text-gray-600 font-bold text-1xl">STL-10 Wire rope SS or V:</h2>
            <h2 class="text-gray-600 font-bold text-1xl">{stl_10_value}</h2>
        </div>
    </div>    
</div>
<style>
    .cb-padding { margin-left:20px; }
	.content {
		width: 100%;
		max-width: var(--column-width);
		margin: var(--column-margin-top) auto 0 auto;
	}
    .container-results {
		width: 60%;
        align-content: center;
    }
    .align-results {
        display: flex;
        justify-content: space-between;  
    }
    .align-checkbox {
        display: flex;
        justify-content: center;  
    }
    h2 { text-align: center; }
</style>