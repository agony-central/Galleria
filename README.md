# Galleria

Ever been bothered by how Sankaku Complex's 3DPD image board, `idol.sankakucomplex.com`, is not only an awful and sucky way to masturbate — but also unsupported by most, third-party, image board-related software?

I have— so here's a UserScript library you can run with Tampermonkey/Greasemonkey to overlay a useful (but kinda' ugly) image gallery. We are at the first version of Galleria, where it works yet isn't in its most convenient state.

## Install

1. Install a UserScript manager

    - as of 2022, I recommend [Tampermonkey](https://www.tampermonkey.net/)

2. Install Galleria

    - simply open [`index.js`'s RAW file](https://raw.githubusercontent.com/agony-central/galleria/master/index.js) in a new window

    - if your UserScript manager doesn't auto-prompt you to install Galleria, it may not be properly installed — please make sure it is enabled and visible in your browser's extensions list

    - alternatively, your UserScript manager may have auto-install disabled, and it may need to have this UserScript installed explicitly — please consult your UserScript manager's documentation if you believe that to be the case

## Why? (Challenges)

While `chan.sankakucomplex.com` provides public, beta access to an in-development version of the image board website — with a slick user interface, and a convenient, gallery view — the `idol.sankakucomplex.com` portion receives no such treatment.

Furthermore, the image board has tight, network security policies in-place that discourage most image board viewers and downloaders.

I believe the server uses the HTTP session cookies in conjuction with the `Referer`\[sic\] HTTP header to prevent cross-loading of post (media) resources from a client location other than the posts' page itself. In other words, an AJAX request to a post's, scraped image link fails — while I have no reason to believe this would fail from the post's page itself, I haven't tried that, but it definitely fails from the search page.

## How? (Solutions)

As such, my current, naive solution is to simply make an `iframe` to hold the entire post's page and switch it as the Galleria user moves between posts.

Finally, the search page for `idol.sankakucomplex.com` auto-pages — and while we could disable it and paginate traditionally, I've instead writting a simple loader routine that can periodically scroll to the bottom of the page — and ensure that we have enough posts available in the buffer for the user to keep looking ahead.

## Features

The gallery is designed with minimal intrusion of the original site's functions in mind, as well as easy navigation:

-   the program will auto-load new posts when it begins to run out
-   common keybinds for easy navigation:
    1. arrow keys
    2. WASD

## Caveats (Improvements)

This is the most incomplete, MVP version of the gallery as it is missing many quality-of-life features. Some features that would improve this plugin:

-   in-gallery searching
-   auto-scrolling of the thumbnail previews
-   a visible index and count of all, loaded posts
-   pruning of the `iframe` to remove unneeded content
-   disable auto-scrolling when the gallery is not in-view
-   user configuration for various aspects of the gallery
    1. keybinds
    2. rate limits
    3. lookahead posts count
    4. theming (light/dark/custom accents)
-   finally, there can also be DevOps and architectural changes to help build and maintain this project better
    1. module-based build system
       a. Rollup.js
       b. Vite
    2. TypeScript support/usage
       a. proper typings for `globalStore`
    3. better seperation of concerns between logic and view (part of modularization)
