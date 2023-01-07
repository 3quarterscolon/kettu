<script lang="ts">
    export let project;
</script>

<div class="project-card">
    <img src="{project.image}" alt="" class="project-thumb">
    <div class="project-text">
        <b class="project-title">{project.title}</b><br>
        <span class="project-author">by {project.author.username}</span>
    </div>
</div>

<style>
    .project-card {
        position: relative;
        text-align: center;
        width: 100%;
        border-radius: 1em;
        border-color: var(--fg);
        border-width: 0.5em;
        transition-duration: 0.2s;
    }

    .project-card:hover {
        border-color: var(--accent);
        border-width: 1em;
    }

    .project-thumb {
        width: 100%;
        border-radius: 1em;
    }

    .project-text {
        position: absolute;
        width: 80%;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background-color: rgba(235, 219, 210, 0.75);
        border-radius: 0.5em;
    }

    .project-title {
        color: var(--accent-dark);
        width: 100%;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
        display: inline-block;
        margin: none;
    }

    .project-author {
        color: var(--gray);
        width: 100%;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
        display: inline-block;
        margin: none;
    }
</style>