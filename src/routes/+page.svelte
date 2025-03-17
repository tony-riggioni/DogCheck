<script>
    import * as m from "../lib/paraglide/messages.js"
    import TopNav from "../components/TopNav.svelte";

    import {onMount} from "svelte";

    onMount(() => {
        document.title = m.LOGIN() // Workaround for a Svelte bug that causes rendering to crash

        const loginForm = document.getElementById("login-form");
        loginForm?.addEventListener("submit", (e) => {
            e.preventDefault();
            sendLoginData(new FormData(loginForm));
        });
    })

    async function sendLoginData(formData) {

        let postBody = {};

        postBody.name = formData.get("username");
        postBody.email = formData.get("email");

        try {
            const response = await fetch("https://frontend-take-home-service.fetch.com", {
                method: "POST",
                body: postBody,
            });
            if (!response.ok)
            {
                const errortext = document.getElementById("errortext");
                errortext.innerText = m.INVALID_CREDS();
            }
        }
        catch (e) {
            console.error(e);
        }
    }

</script>
<head>
    <link rel="stylesheet" href="colours.css">
</head>

<TopNav></TopNav>

<h1>{m.SITE_WELCOME()}</h1>
<div class="median-centre">
    <p>{m.PLEASE_LOGIN()}</p>
    <form id="login-form">
        <label for="username">{m.USERNAME()}:</label>
        <input type="text" id="username" name="username"><br><br>
        <label for="email">{m.EMAIL()}:</label>
        <input type="text" id="email" name="email"><br><br>
        <input type="submit" value={m.LOGIN()}>
    </form>
    <p id="errortext"></p>
</div>

<style>
    h1 {
        text-align: center;
    }

    .median-centre {
        position: relative;
        width: 50%;
        left: 25%;
        overflow: auto;
        align-content: center;
    }

    #errortext {
        color: red;
        font-size: 25px;
    }
</style>
