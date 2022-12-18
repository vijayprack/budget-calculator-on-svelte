<script>
    async function getUsers() {
        let userData = await fetch('https://api.github.com/users');
        let githubUsers = await userData.json();
        return githubUsers;
    };
</script>

<section>
    {#await getUsers()}
    <!-- promisis pending -->
    <h1>Loading...</h1>
    {:then users} 
        {#each users as user}
            <article class="user">
                <img src={user.avatar_url} alt={user.login}>
                <div class="user_info">
                    <h3>User : {user.login}</h3>
                    <a href={user.html_url} class="btn-primary" target="blank">
                    github url</a>
                </div>
            </article>
        {/each}
        {:catch error}
            <!-- promis was rejected -->
            <p>Something was wrong : {error.message}</p>
    {/await}
</section>