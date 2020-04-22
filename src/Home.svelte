<script>
    import Profile from './components/Profile.svelte';
    import GameList from './components/GameList.svelte';
    export let user;
    export let firebase;
</script>

<div>
    <Profile {user}/>
    <GameList {user} {firebase}/>
</div>