<script lang="ts">

    // STATE
    let result = $state('');
    let xValue = $state(10);

    let totalHeads = $state(0);
    let totalTails = $state(0);

    let krarksThumb = $state(false);

    // BASIC FLIP
    function basicFlip(): string {
        return Math.random() < 0.5 ? 'Heads' : 'Tails';
    }

    // KRARK'S THUMB LOGIC
    function performFlip(): string {

        if (!krarksThumb) {
            return basicFlip();
        }

        const flip1 = basicFlip();
        const flip2 = basicFlip();

        return (flip1 === 'Heads' || flip2 === 'Heads')
            ? 'Heads'
            : 'Tails';
    }

    // UPDATE STATS
    function updateStats(flip: string) {

        if (flip === 'Heads') {
            totalHeads++;
        } else {
            totalTails++;
        }
    }

    // SINGLE FLIP
    function singleFlip() {

        const flip = performFlip();

        updateStats(flip);

        result = `Result: ${flip}`;
    }

    // FLIP X COINS
    function flipXCoins() {

        let heads = 0;
        let tails = 0;

        for (let i = 0; i < xValue; i++) {

            const flip = performFlip();

            if (flip === 'Heads') heads++;
            else tails++;

            updateStats(flip);
        }

        result = `Flipped ${xValue} coins\nHeads: ${heads}\nTails: ${tails}`;
    }

    // FLIP UNTIL FAILURE
    function flipUntilFailure() {

        let streak = 0;

        while (true) {

            const flip = performFlip();

            updateStats(flip);

            if (flip === 'Tails') break;

            streak++;
        }

        result = `Survived ${streak} flips before Tails`;
    }

    // FLIP UNTIL SUCCESS
    function flipUntilSuccess() {

        let attempts = 0;

        while (true) {

            const flip = performFlip();

            updateStats(flip);

            attempts++;

            if (flip === 'Heads') break;
        }

        result = `Took ${attempts} flips to reach Heads`;
    }

    // RESET COUNTERS
    function resetCounters() {

        result = '';
        totalHeads = 0;
        totalTails = 0;
        xValue = 10;
        krarksThumb = false;
    }

</script>

<div class="container">

    <h1>Coin Flip Simulator</h1>

    <div class="controls">

        <button onclick={singleFlip}>
            Flip One Coin
        </button>

        <div class="x-flip">

            <input
                type="number"
                min="1"
                bind:value={xValue}
            />

            <button onclick={flipXCoins}>
                Flip X Coins
            </button>

        </div>

        <button onclick={flipUntilFailure}>
            Flip Until Failure
        </button>

        <button onclick={flipUntilSuccess}>
            Flip Until Success
        </button>

        <button onclick={() => krarksThumb = !krarksThumb}>
            Krark's Thumb:
            {krarksThumb ? 'ON' : 'OFF'}
        </button>

        <!-- NEW RESET BUTTON -->
        <button onclick={resetCounters} class="reset">
            Clear / Reset
        </button>

    </div>

    <div class="results">

        <h2>Results</h2>

        <p>{result}</p>

        <div class="stats">
            <p>Total Heads: {totalHeads}</p>
            <p>Total Tails: {totalTails}</p>
        </div>

        <div class="probability">

            {#if krarksThumb}
                <p>Krark's Thumb Active</p>
                <p>Heads chance increased</p>
            {:else}
                <p>Normal Probability</p>
            {/if}

        </div>

    </div>

</div>

<style>

    .container {
        display: flex;
        flex-direction: column;
        align-items: center;
        margin-top: 60px;
        font-family: Arial, sans-serif;
    }

    .controls {
        display: flex;
        flex-direction: column;
        gap: 15px;
        width: 320px;
    }

    .x-flip {
        display: flex;
        gap: 10px;
    }

    input {
        width: 100px;
        padding: 12px;
        font-size: 16px;
        border-radius: 10px;
        border: 1px solid #ccc;
    }

    button {
        padding: 14px;
        font-size: 16px;
        border: none;
        border-radius: 12px;
        cursor: pointer;
        background-color: #222;
        color: white;
        transition: 0.2s;
    }

    button:hover {
        transform: scale(1.03);
    }

    .reset {
        background-color: #b00020;
    }

    .results {
        margin-top: 40px;
        text-align: center;
        max-width: 500px;
    }

    .stats {
        margin-top: 20px;
    }

    p {
        white-space: pre-line;
    }

</style>