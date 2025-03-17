<script module>
    import * as m from "../lib/paraglide/messages.js"

    let username = '';
</script>

<script lang="ts">
    import type { AvailableLanguageTag } from '$lib/paraglide/runtime';
    import { i18n } from '$lib/i18n';
    import { page } from '$app/state';
    import { goto } from '$app/navigation';

    function switchLang(lang: AvailableLanguageTag) {
        const canonicalPath = i18n.route(page.url.pathname);
        const localPath = i18n.resolveRoute(canonicalPath, lang);
        goto(localPath);
    }
    function welcomeUser(user: string): string
    {
        if (user == '') {
            return m.LOGIN(); // Top Bar reads Welcome, Login before user logs in
        }
        return user;

    }
</script>

<div class="topnav">
    <div class="left-align">{m.WELCOME({user: welcomeUser(username)})}</div>
    <div class="center-align top-title">{m.PUNNAME()}</div>
    <button class="right-align" onclick={() => switchLang('en')}>English</button>
    <button class="right-align" onclick={() => switchLang('es')}>Español</button>
</div>

<style>
    .topnav {
        background-color: #333;
        overflow: hidden;
        flex: auto;
    }

    .topnav button,div {
        padding: 14px 16px;
        font-size: 17px;
        color: #fafafa;
        border: none;
        background: #333 none;
    }

    .topnav .right-align {
        float: right;
    }

    .topnav .center-align {
        position: absolute;
        float: left;
        left: 46%;
        text-align: center;
    }

    .topnav .left-align {
        float: left;
    }

    .topnav .top-title {
        padding-top: 10px;
        font-size: 25px;
    }

</style>
