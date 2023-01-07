<html lang="en">
    <h1>Welcome to Kettu!</h1>
    <p>Choose somewhere to visit!</p>
    <ul id="visit-sel">
        <li class="btn-left">
            <input type="radio" name="visit" id="projects" on:click="{() => visit_location = 'Projects'}">
            <label for="project">Projects</label>
        </li>
        <li>
            <input type="radio" name="visit" id="studios" on:click="{() => visit_location = 'Studios'}">
            <label for="project">Studios</label>
        </li>
        <li>
            <input type="radio" name="visit" id="profiles" on:click="{() => visit_location = "Profiles"}">
            <label for="project">Profiles</label>
        </li>
        <li class="btn-right">
            <input type="radio" name="visit" id="posts" on:click="{() => visit_location = "Posts"}">
            <label for="project">Posts</label>
        </li>
    </ul>
    {#if visit_location == "Projects"}
        {#await getProjects()}
            <!-- request is pending -->
            <p>Loading projects...</p>
        {:then projects}
            <!-- request was fulfilled -->
            <div class="project-grid">{#each projects as project}<Project {project} />{/each}</div>
        {:catch error}
            <!-- request was rejected -->
            <p>Oops! Something went wrong: {error.message}</p>
    {/await}
    {:else if visit_location == "None"}
        <p>Select something to start!</p>
    {:else}
        <p>{visit_location} are coming soon!</p>
    {/if}
</html>

<script lang="ts">
    import Project from './project.svelte'

    let visit_location = "None";

    async function getProjects() {
        let response = await fetch("https://scratchproxy.deta.dev/explore/projects?q=games&mode=trending&language=en") 
        if (response.ok) {
            return response.json();
        }
        throw new Error('API fetch failed.'); 
    }
</script>

<style>

    /* Variable and font setup */

    :root {
        --bg: #282828;
        --fg: #ebdbd2;
        --accent: #fe8019;
        --accent-dark: #d65d0e;
        --bg1: #3c3836;
        --bg2: #504945;
        --bg3: #665c54;
        --bg4: #7c6f64;
        --gray: #928374;
        --red: #fb4934;
        --green: #b8bb26;
        --yellow: #fabd2f;
        --blue: #83a598;
        --purple: #53869b;
        --aqua: #8ec07c;
    }

    @font-face {
        font-family: Poppins;
        src: url(../fonts/Poppins-Medium.ttf);
    }

    @font-face {
        font-family: Poppins;
        src: url(../fonts/Poppins-Bold.ttf);
        font-weight: bold;
    }

    @font-face {
        font-family: Unbounded;
        src: url(../fonts/Unbounded-Black.ttf);
    }

    /* Element theming */

    html {
        background-color: var(--bg);
        color: var(--fg);
        font-family: Poppins, sans-serif;
        padding: 1em
    }

	h1 {
		color: var(--accent);
        text-align: center;
		font-family: Unbounded, cursive;
		font-size: 3em;
	}

    p {
        font-size: 1em;
    }

    /* This is the code that makes the radiobox list look like buttons.
       Don't know how it works, but it does. TODO: clean this up.       */

    #visit-sel {
        list-style-type:none;
        width: 100%;
        height: 2em;
        padding: 0;
    }

    #visit-sel li {
        background: var(--bg1);
        float: left;
        width: 25%;
        height: 100%;
        font-size: 1.5em;
        position: relative;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    #visit-sel li.btn-left, #visit-sel li.btn-left label {
        border-radius: 0.5em 0em 0em 0.5em;
    }

    #visit-sel li.btn-right, #visit-sel li.btn-right label {
        border-radius: 0em 0.5em 0.5em 0em;
    }

    #visit-sel label, #visit-sel input {
        position: absolute;
        width: 100%;
        height: 100%;
        text-align: center;
    }

    #visit-sel label {
        border-width: 0.1em;
        border-color: var(--gray); 
        font-family: Unbounded, cursive;
        cursor: pointer;
        z-index: 90;
    }

    #visit-sel li:hover {
        background: var(--bg2);
        transition-duration: 0.2s;
    }

    #visit-sel input[type="radio"]:checked + label {
        background: var(--accent);
        color: var(--bg);
        transition-duration: 0.2s;
    }

    #visit-sel input[type="radio"]:checked:hover + label {
        background: var(--accent-dark);
        color: var(--bg);
        transition-duration: 0.2s;
    }

    #visit-sel input[type="radio"] {
        opacity: 0.01;
        z-index: 100;
    }

    .project-grid {
        display: grid;
        width: 100%;
        grid-template-columns: auto auto auto auto;
        gap: 10px;
    }
</style>