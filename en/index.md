---
_layout: landing
---

<section class="watson-banner">
    <section class="container-xxl">
        <h1>Watson Documentation</h1>
        <p style="max-width: 750px">
            This website includes all the documentation for the Watson Mixed Reality project.
            Here you can read up on the purpose of this project and the technical documentation 
            for the prototype application.
        </p>
        <section class="banner-action">
            <a href="./docs/introduction.html">
                <button>
                    Open Docs
                </button>
            </a>
            <a href="https://github.com/XR-Solutions">
                <button>
                    View repositories
                </button>
            </a>
        </section>
    </section>
</section>
<div class="space-maker"></div>

<style>
    .watson-banner {
        position: absolute;
        width: 100vw;
        min-height: 600px;
        top: 60px;
        left: 0px;
        background: url('../images/banner/banner-2.png');
        background-size: cover;
        background-position: center;
        border-bottom: solid 1px var(--bs-border-color);
        display: flex;
        align-items: center;
    }

    .watson-banner h1, .watson-banner p {
        color: #EFEFEF;
    }

    .banner-action {
        display: flex;
        gap: 15px;
    }

    .banner-action button {
        text-decoration: none;
        border: solid 1px var(--bs-border-color);
        background: var(--bs-secondary-bg);
        padding: 5px 20px;
        border-radius: 5px;
        transition: background 0.3s;
    }

    .banner-action button:hover {
        background: var(--bs-tertiary-bg);
    }

    .banner-action a::after {
        display: none !important;
    }

    .space-maker {
        margin-bottom: 700px;
    }
</style>

## Team
The team exists of Romano, Kadir, Joyson and Brandon.
