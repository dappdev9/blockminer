<script>
    import Game from './Game.svelte';
    import {Doc, Collection} from 'sveltefire';
    export let user;
    export let firebase;

    let db = firebase.firestore();

    let gameStart = false;
    let gameRef;

    let newGame = {
        status: 'recruiting',
        author: user.uid,
        miners: []
    }

    function connectToGame(ref) {
        console.log(ref)
        // db.collection('users').doc(user.uid)
        // .get()
        // .then(function(doc) {
        //     if (doc.exists) {
        //         console.log("Document data:", doc.data());
        //     } else {
        //         // doc.data() will be undefined in this case
        //         console.log("No such document!");
        //     }
        // }).catch(function(error) {
        //     console.log("Error getting document:", error);
        // });
    }

    function startGame(ref) {

        gameRef = ref;
        console.log(ref)
        gameStart = true;
    }

</script>

<!-- {#if gameStart}
    <Game {gameRef}/>
{/if} -->

<Doc path={`users/${user.uid}`} let:data>
    <p>
        Game list
    </p>
    <div>
        <div>
            <Collection path={`games/star/${data.player.location.star}/planet/${data.player.location.planet}`}
            let:data={games} let:ref>
                <p>
                    Games:
                </p>

                {#if games.length >= 1}
                <ul>
                    {#each games as g}
                    <li>
                        {g.author} {g.status} {g.miners.length}

                        {#if g.miners.includes(user.uid)}
                        <button on:click={()=> g.ref.update({miners: firebase.firestore.FieldValue.arrayRemove(user.uid)})}>
                        Disconnect
                        </button>
                        {:else}
                        <button on:click={()=> g.ref.update({miners: firebase.firestore.FieldValue.arrayUnion(user.uid)})}>
                        Connect
                        </button>
                        {/if}

                        {#if g.author == user.uid && g.miners.length >= 1}
                        <button on:click={()=> g.ref.update({status: 'started'})}>
                        Start
                        </button>
                        {/if}

                        {#if g.status === 'started'}
                            <Game {user} gameref={g.ref}/>
                        {/if}

                    </li>
                    {/each}
                </ul>
                {/if}
                <hr>
                <div>
                    <button on:click={()=> ref.add(newGame)}>new game</button>
                </div>
            </Collection>
        </div>
    </div>
</Doc>