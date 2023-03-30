<script lang="ts">
    import { onMount } from "svelte";

    import svelteLogo from "./assets/svelte.svg";
    import viteLogo from "/vite.svg";
    import Counter from "./lib/Counter.svelte";
    import HelloWorld from "./js/Pages/Hello/World.svelte";
    import HelloToo from "./js/Pages/Hello/Worldtoo.svelte";
    import axios from "axios";
    const endpointoo = "https://jsonplaceholder.typicode.com/posts";
    const endpoint3 = "http://localhost:8000/api/world";
    const endpointworld = "world";

    const headers = {
        "Access-Control-Allow-Origin": "http://localhost:8000",
        "Access-Control-Allow-Methods": "GET,PUT,POST,DELETE,OPTIONS",
        "Access-Control-Allow-Headers": "Content-Type",
        "Content-Type": "application/json",
        Authorization: "localstorage access token",
        //"Authorization": `Bearer ${localStorage.getItem("access_token")}`,
    };

    //axios install seems to be fine no TypeDef error
    // "http://localhost:8000/api/" is .env
    const service = axios.create({
        headers: headers,
        baseURL: import.meta.env.VITE_LOCAL_API_ENDPOINT,
        timeout: 3000,
    });
    console.log(service);
    console.log("service displayed");
    let hiddenenvvar = import.meta.env.LOCAL_API_ENDPOINT;
    console.log(hiddenenvvar);
    console.log(import.meta.env.VITE_LOCAL_API_ENDPOINT);
    console.log(import.meta.env.MODE); // development or production

    let topposts = [];
    let what;

    onMount(async function () {
        try {
            const response = await axios.get(endpointoo);
            console.log(response.data);

            const response2 = await service.get(endpointworld);
            console.log(response2.data);
            //name = response2.data;
            what = response2.data;

            //topposts = response.data;
        } catch (error) {
            console.error(error);
        }
    });
</script>

<main>
    <div>
        <a href="https://vitejs.dev" target="_blank" rel="noreferrer">
            <img src={viteLogo} class="logo" alt="Vite Logo" />
        </a>
        <a href="https://svelte.dev" target="_blank" rel="noreferrer">
            <img src={svelteLogo} class="logo svelte" alt="Svelte Logo" />
        </a>
    </div>
    <h1>Vite + Svelte</h1>
    <div class="card">
        <HelloWorld name={what} />
    </div>
    <div class="card">
        <HelloToo />
    </div>
    <div class="card">
        <Counter />
    </div>
    {#each topposts as article}
        <div>
            <p>{article.title}</p>
        </div>
    {/each}
    <p>
        Check out <a href="https://github.com/sveltejs/kit#readme" target="_blank" rel="noreferrer">SvelteKit</a>, the
        official Svelte app framework powered by Vite!
    </p>

    <p class="read-the-docs">Click on the Vite and Svelte logos to learn more</p>
</main>

<style>
    .logo {
        height: 6em;
        padding: 1.5em;
        will-change: filter;
        transition: filter 300ms;
    }
    .logo:hover {
        filter: drop-shadow(0 0 2em #646cffaa);
    }
    .logo.svelte:hover {
        filter: drop-shadow(0 0 2em #ff3e00aa);
    }
    .read-the-docs {
        color: #888;
    }
</style>
