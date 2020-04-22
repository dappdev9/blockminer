<script>
    import {Doc, Collection} from 'sveltefire';
    export let user;

    let player = {
        name: 'player name',
        balance: 1000,
        location: {
            star: 'sun',
            planet: 'earth'
        }
    }

    function createPlayer() {

    }
</script>

<div>
    <div>
        <p>
            User email: {user.email}
        </p>
        <p>
            User uid: {user.uid}
        </p>
    </div>
    <div>
        <Doc path={`users/${user.uid}`} let:data let:ref>

            <div slot="fallback">
                <p>
                    Придумайте имя игрока:
                </p>
                <Collection path={'users'} let:ref>
                    <input type="text" bind:value={player.name}>
                    <button on:click={() => ref.doc(user.uid).set({player})}>Создать</button>
                </Collection>
            </div>

            <div>
                <p>
                    Player name: {data.player.name}
                </p>
            </div>
        </Doc>
    </div>
</div>