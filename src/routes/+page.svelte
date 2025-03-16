<script>
    import * as m from "../lib/paraglide/messages.js"
    import TopNav from "../components/TopNav.svelte";

    document.title = m.LOGIN() // Workaround for a Svelte bug that causes rendering to crash
</script>
<head>
    <link rel="stylesheet" href="colours.css">
</head>

<TopNav></TopNav>

<h1>{m.SITE_WELCOME()}</h1>
<div class="median-centre">
    <p>{m.PLEASE_LOGIN()}</p>
</div>

<style>
    h1 {
        text-align: center;
    }

    .median-centre {
        flex: auto;
        width: 85%;
        overflow: auto;
        align-content: center;
    }
</style>
