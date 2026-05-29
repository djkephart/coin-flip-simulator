<script lang="ts">

    let darkMode = $state(true);

    let result = $state('');
    let xValue = $state(10);

    let totalHeads = $state(0);
    let totalTails = $state(0);

    let krarksThumb = $state(false);

    type HistoryEntry = {
        text: string;
        krark: boolean;
    };

    let history = $state<HistoryEntry[]>([]);

    function basicFlip(): string {
        return Math.random() < 0.5 ? 'Heads' : 'Tails';
    }

    function performFlip(): string {

        if (!krarksThumb) return basicFlip();

        const f1 = basicFlip();
        const f2 = basicFlip();

        return (f1 === 'Heads' || f2 === 'Heads')
            ? 'Heads'
            : 'Tails';
    }

    function updateStats(flip: string) {
        if (flip === 'Heads') totalHeads++;
        else totalTails++;
    }

    function log(entry: string) {
        history = [
            { text: entry, krark: krarksThumb },
            ...history
        ].slice(0, 20);
    }

    function singleFlip() {
        const flip = performFlip();
        updateStats(flip);
        result = `One Coin : ${flip}`;
        log(`Flip One Coin → ${flip}`);
    }

    function flipXCoins() {

        let heads = 0;
        let tails = 0;

        for (let i = 0; i < xValue; i++) {
            const flip = performFlip();
            if (flip === 'Heads') heads++;
            else tails++;
            updateStats(flip);
        }

        const msg = `Flip X (${xValue}) Coins → H:${heads} T:${tails}`;
        result = msg;
        log(msg);
    }

    function flipUntilFailure() {

        let streak = 0;

        while (true) {
            const flip = performFlip();
            updateStats(flip);
            if (flip === 'Tails') break;
            streak++;
        }

        const msg = `Flip Until Failure → ${streak} success flips`;
        result = msg;
        log(msg);
    }

    function flipUntilSuccess() {

        let attempts = 0;

        while (true) {
            const flip = performFlip();
            updateStats(flip);
            attempts++;
            if (flip === 'Heads') break;
        }

        const msg = `Flip Until Success → ${attempts} flips`;
        result = msg;
        log(msg);
    }

    function reset() {
        result = '';
        xValue = 10;
        totalHeads = 0;
        totalTails = 0;
        krarksThumb = false;
        history = [];
    }

    function winRate() {
        const total = totalHeads + totalTails;
        return total ? (totalHeads / total) * 100 : 0;
    }

</script>

<div class:dark={darkMode} class="page">

    <h1 class="title">Coin Flip Simulator</h1>
    <p class="subtitle">A coin flip simulator intended for Magic: The Gathering</p>

    <div class="stack">

        <div class="card">
            <h2>Controls</h2>

            <button onclick={singleFlip}>Flip One Coin</button>

            <div class="row">
                <input type="number" min="1" bind:value={xValue} />
                <button onclick={flipXCoins}>Flip X</button>
            </div>

            <button onclick={flipUntilFailure}>Flip Until Failure</button>
            <button onclick={flipUntilSuccess}>Flip Until Success</button>

            <div class="krark-wrap">

                <button onclick={() => krarksThumb = !krarksThumb}>
                    Krark’s Thumb: {krarksThumb ? 'ON' : 'OFF'}
                </button>

                <img
                    class="krark-preview"
                    src="/krarks-thumb.jpg"
                    alt="Krark's Thumb"
                />

            </div>

            <button class="reset" onclick={reset}>
                Reset All
            </button>
        </div>

        <div class="card">
            <h2>Results</h2>

            <p><b>Latest:</b> {result}</p>
            <p>Heads: {totalHeads}</p>
            <p>Tails: {totalTails}</p>
            <p>Win Rate: {winRate().toFixed(1)}%</p>
        </div>

        <div class="card">
            <h2>History</h2>

            {#if history.length === 0}
                <p class="muted">No flips yet</p>
            {:else}
                <ul>
                    {#each history as h}
                        <li>
                            {h.text}
                            <span class="tag">
                                {h.krark ? ' (Krark ON)' : ' (Krark OFF)'}
                            </span>
                        </li>
                    {/each}
                </ul>
            {/if}
        </div>

    </div>

    <button class="toggle" onclick={() => darkMode = !darkMode}>
        {darkMode ? 'Dark Mode 🌙' : 'Light Mode ☀️'}
    </button>

</div>

<style>

/* RESET */
:global(body) {
    margin: 0;
}

/* PAGE */
.page {
    font-family: Arial, sans-serif;
    padding: 40px;
    display: flex;
    flex-direction: column;
    align-items: center;
    min-height: 100vh;
    transition: background 0.3s ease, color 0.3s ease;
}

/* THEMES */
.page.dark {
    background: #0f1115;
    color: white;
}

.page:not(.dark) {
    background: #f3f5f8;
    color: #111;
}

/* TITLE */
.title {
    text-align: center;
    margin-bottom: 5px;
}

.subtitle {
    text-align: center;
    margin-bottom: 25px;
    opacity: 0.7;
}

/* STACK */
.stack {
    display: flex;
    flex-direction: column;
    gap: 20px;
    width: 100%;
    max-width: 520px;
}

/* CARD */
.card {
    padding: 20px;
    border-radius: 16px;
}

.card h2 {
    width: 100%;
    text-align: center;
    margin: 0 0 12px 0;
}

/* THEMES */
.page.dark .card {
    background: rgba(255,255,255,0.06);
    border: 1px solid rgba(255,255,255,0.1);
}

.page:not(.dark) .card {
    background: white;
    border: 1px solid #e5e5e5;
}

/* BUTTONS */
button {
    width: 100%;
    margin: 6px 0;
    padding: 12px;
    border-radius: 12px;
    border: none;
    cursor: pointer;
    background: #2b3550;
    color: white;
    transition: background 0.25s ease, transform 0.15s ease;
}

.page:not(.dark) button {
    background: #2f3b52;
}

/* RESET */
.reset {
    background: #d64545;
}

.page:not(.dark) .reset {
    background: #c03939;
}

/* TOGGLE */
.toggle {
    margin-top: 25px;
    width: auto;
    padding: 8px 14px;
    font-size: 13px;
    border-radius: 10px;
    background: #444;
}

/* KRARK WRAP */
.krark-wrap {
    position: relative;
}

/* HOVER IMAGE */
.krark-preview {
    position: absolute;
    top: -10px;
    left: 105%;
    width: 280px;
    opacity: 0;
    transform: scale(0.95);
    transition: 0.2s ease;
    border-radius: 10px;
    pointer-events: none;
    border: 1px solid rgba(255,255,255,0.2);
}

.krark-wrap:hover .krark-preview {
    opacity: 1;
    transform: scale(1);
}

/* INPUT */
.row {
    display: flex;
    gap: 10px;
}

input {
    flex: 1;
    padding: 12px;
    border-radius: 10px;
    border: 1px solid #ccc;
}

/* HISTORY */
ul {
    text-align: left;
    max-height: 250px;
    overflow-y: auto;
    padding-left: 15px;
}

.muted {
    opacity: 0.6;
}

.tag {
    opacity: 0.6;
    font-size: 12px;
    margin-left: 6px;
}

</style>