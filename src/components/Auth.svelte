<script>
    export let auth;

    let email = '';
    let password = '';

    function signIn() {
        auth.signInWithEmailAndPassword(email, password).catch(function(error) {
        // Handle Errors here.
        var errorCode = error.code;
        var errorMessage = error.message;
        // ...
        });
    }

    function signUp() {
        auth.createUserWithEmailAndPassword(email, password).catch(function(error) {
        // Handle Errors here.
        var errorCode = error.code;
        var errorMessage = error.message;
        // ...
        });
    }
</script>

<div>
    <div>
        <input type="text" bind:value={email}>
        <input type="text" bind:value={password}>
        <button on:click={signIn}>SignIn</button>
        <button on:click={signUp}>SignUp</button>
    </div>
</div>