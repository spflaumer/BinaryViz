<style>
.bdigit-list {
    display: flex;
    flex-direction: row;
    justify-content: center;
    margin: auto;
    max-width: 98%;
    margin: auto;
    flex-wrap: wrap;
}

.bdigit {
    appearance: unset;
    border: none;
    margin: 0.3rem;
    padding: 0rem 0.3rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    color: #b4befe;
    background-color: #313244;
    border-radius: 24px;
}

.bdigit-val {
    font-size: 2rem;
    margin: 12px 8px 4px 8px;
}

.ddigit-val {
    font-size: 1rem;
    margin: 4px 8px 12px 8px;
}

.bdigit-ctl {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
}


.ddigit-total-container {
    margin: auto;
    align-items: center;
    display: flex;
    flex-direction: column;
}
.ddigit-total {
    color: #cdd6f4;
    font-size: 2rem;
    margin: 16px;
}
.ddigit-bitwidth {
    color: #cdd6f4;
    font-size: 1rem;
    margin: 16px;
}

#add-bdigit, #rem-bdigit {
    appearance: unset;
    color: #cdd6f4;
    background-color: #11111b;
    border: none;
    margin: 8px;
    font-size: 1.5rem;
    width: 2rem;
    height: 2rem;
    border-radius: 24px;
}

</style>

<main>
<div class="bdigit-list">
    {#each digits as digit, idx}
            <button class="bdigit" on:click={toggle_digit(idx)}>
                    <p class="bdigit-val">{digit}</p>
                    <p class="ddigit-val">{digit * Math.pow(2, digits.length - idx - 1)}</p>
            </button>
    {/each}
</div>

<div class="ddigit-total-container">
        <p class="ddigit-total">{sum}</p>
        <p class="ddigit-bitwidth">Bit width: {digits.length}</p>
</div>

<div class="bdigit-ctl">
    <button id="add-bdigit" on:click={add_digit}>+</button>
    <button id="rem-bdigit" on:click={rem_digit}>-</button>
</div>
</main>

<script>

/**
 * @type Array<number>
 */
let digits = [0];
$: sum = digits.reduce((acc, v, idx) => acc + (v * Math.pow(2, digits.length - 1 - idx)), 0)

/**
 * @param {number} idx
 */
function toggle_digit(idx) {
    return () => {
        let digs = digits
        digs[idx] = (digs[idx] + 1) % 2;
        digits = digs
    }
}

function add_digit() {
    digits = [0, ...digits];
}

function rem_digit() {
    if(digits.length < 2) return;

    let digs = digits;
    digs.shift();
    digits = digs;
}
</script>
