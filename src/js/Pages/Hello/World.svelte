<script>
    import Logo from "../Shared/Logo.svelte";

    import { onMount } from "svelte";
    const endpoint = "https://jsonplaceholder.typicode.com/posts";
    let posts = [];

    onMount(async function () {
        const response = await fetch(endpoint);
        const data = await response.json();
        console.log(data);
        posts = data;
    });

    export let name;
    //export let topposts;
</script>

<svelte:head>
    <title>Login - Ping CRM</title>
</svelte:head>

<main>
    <div class="p-6 bg-indigo-800 min-h-screen flex justify-center items-center">
        <div class="w-full max-w-md">
            <Logo class="block mx-auto w-full max-w-xs fill-white" height="50" />
        </div>

        <h1>Hello {name}!</h1>
        {#each posts as article}
            <div>
                <p>{article.title}</p>
            </div>
        {/each}
        <p>
            Visit the
            <a href="https://svelte.dev/tutorial">Svelte tutorial</a>
            to learn how to build Svelte apps.
        </p>
    </div>
</main>
