<script>
    // export let firebase;
    export let user;

    export let gameref;

    console.log(user, gameref);

    let playerSecret;
    let gameSecret;
    
</script>

<div id="game">
    <div>
        <p>
        GAME START
        </p>
    </div>
    <div>
        <input type="text" bind:value={playerSecret}>
        <button on:click={console.log('ok')}>ok</button>
    </div>
</div>

<style>
    #game {
        position: absolute;
        left: 50%;
        transform: translateX(-50%);
        border: solid;
        border-radius: 15px;
        background-color: burlywood;
        box-shadow: 5px, 5px, 20px, black;
        padding: 3px;
    }
</style>