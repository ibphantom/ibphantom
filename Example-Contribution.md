<h1 align="center">Wizarr</h1>
<h3 align="center">The Free Media Invitation System</h3>

---

<p align="center">
<img src="https://github.com/Wizarrrr/wizarr/blob/master/screenshots/wizard.png?raw=true" height="200">
<br/>
<br/>
<a href="https://github.com/wizarrrr/wizarr">
<img alt="GPL 2.0 License" src="https://img.shields.io/github/license/wizarrrr/wizarr.svg"/>
</a>
<a href="https://github.com/Wizarrrr/wizarr/releases">
<img alt="Current Release" src="https://img.shields.io/github/release/wizarrrr/wizarr.svg"/>
</a>
<a href="https://hosted.weblate.org/engage/wizarr/">
<img src="https://hosted.weblate.org/widgets/wizarr/-/app/svg-badge.svg" />
</a>
<a href="https://opencollective.com/wizarr">
<img alt="Donate" src="https://img.shields.io/opencollective/all/wizarr.svg?label=backers"/>
</a>
<a href="https://features.wizarr.dev">
<img alt="Submit Feature Requests" src="https://img.shields.io/badge/vote_now-features?label=features"/>
</a>
<a href="https://discord.gg/XXCz7aM3ak">
<img alt="Chat on Discord" src="https://img.shields.io/discord/1020742926856372224"/>
</a>
<a href="https://www.reddit.com/r/wizarr">
<img alt="Join our Subreddit" src="https://img.shields.io/badge/reddit-r%2Fwizarr-%23FF5700.svg"/>
</a>
<a href="https://github.com/Wizarrrr/wizarr/issues">
<img alt="Github Issue" src="https://img.shields.io/github/issues/wizarrrr/wizarr"/>
</a>
<a href="https://github.com/Wizarrrr/wizarr/actions/workflows/docker-build.yml">
<img alt="Github Build" src="https://img.shields.io/github/actions/workflow/status/wizarrrr/wizarr/docker-build.yml"/>
</a>
</p>

---
<h3><p align="center">Table of contents</p></h3>

<p align="center">
---
Welcome to the Wizarr Documentation
---

# Introduction

Wizarr is a automatic user invitation system for Plex, Jellyfin and Emby. Create a unique link and share it to a user and they will automatically be invited to your media Server! They will even be guided to download the client and instructions on how to use your requests software!

### Features

* Automatic Invitation to your Media Server (Plex, Jellyfin, Emby...)
* Secured invitation environment
* Plug and Play SSO Support\*
* Multi-tiered Invitations
* Duration for membership
* Guide user on how to download Plex client
* Requests Integration: Guide users on how to request Movie (Jellyseerr, Overseerr & Ombi)
* Discord Server Integration: Invite users to your Discord Server
* Customizable: Add any Custom HTML</p>

<h3><p align="center">💾 Getting-Started</p></h3>

<p align="center">* [Installation]
### Docker

{% hint style="warning" %}
Be sure to replace`/path/to/appdata/config` in the below examples with a valid host directory path. If this volume mount is not configured correctly, your Wizarr settings/data will not be persisted when the container is recreated (e.g., when updating the image or rebooting your machine).

The `TZ` environment variable value should also be set to the [TZ database name](https://en.wikipedia.org/wiki/List\_of\_tz\_database\_time\_zones) of your time zone!
{% endhint %}

{% tabs %}
{% tab title="Docker Compose (recommended)" %}
**Installation:**

Define the `wizarr` service in your `docker-compose.yml` as follows:

```yaml
---
version: "3.8"
services:
  wizarr:
    container_name: wizarr
    image: ghcr.io/wizarrrr/wizarr
    #user: 1000:1000 #Optional but recommended, sets the user uid that Wizarr will run with
    ports:
      - 5690:5690
    volumes:
      - /path/to/appdata/config:/data/database
    environment:
      - APP_URL=https://wizarr.domain.com #URL at which you will access and share 
      - DISABLE_BUILTIN_AUTH=false #Set to true ONLY if you are using another auth provider (Authelia, Authentik, etc)
      - TZ=Europe/London #Set your timezone here
```

Then, start all services defined in the Compose file:

`docker compose up -d` **or** `docker-compose up -d`

**Updating**

Pull the latest image:

`docker compose pull wizarr` or `docker-compose pull wizarr`

Then, restart all services defined in the Compose file:

`docker compose up -d` or `docker-compose up -d`
{% endtab %}

{% tab title="Docker CLI" %}
**Installation**

<pre class="language-docker"><code class="lang-docker"><strong>docker run -d \
</strong>  --name wizarr \
  -e APP_URL=https://wizarr.domain.com \
  -e DISABLE_BUILTIN_AUTH=false \
  -e TZ=Europe/London \
  -p 5690:5690 \
  -v /path/to/appdata/config:/data/database \
  --restart unless-stopped \
  ghcr.io/wizarrrr/wizarr
</code></pre>

**Updating**

Stop and remove the existing container:

```bash
docker stop wizarr && docker rm wizarr
```

Pull the latest image:

```bash
docker pull ghcr.io/wizarrrr/wizarr
```

Finally, run the container with the same parameters originally used to create the container:

```bash
docker run -d ...
```
{% endtab %}
{% endtabs %}

## Unraid

1. Ensure you have the **Community Applications** plugin installed.
2. Inside the **Community Applications** app store, search for **Wizarr**.
3. Click the **Install Button**.
4. On the following **Add Container** screen, make changes to the **Host Port** and **Host Path 1**(Appdata) as needed, as well as the environment variables.
5. Click apply and access "Wizarr" at your `<ServerIP:HostPort>` in a web browser.
</p>
<p align="center">* [Reverse Proxy](getting-started/reverse-proxy.md)</p>

<h3><p align="center">💭 Using Wizarr</p></h3>

<p align="center">* [Single-Sign-On (SSO)](using-wizarr/single-sign-on-sso.md)</p>
<p align="center">* [Custom HTML](using-wizarr/custom-html.md)</p>
<p align="center">* [Requests Integration](using-wizarr/requests-integration.md)</p>
<p align="center">* [Discord Integration](using-wizarr/discord-integration.md)</p>

<h3><p align="center">⛑ Support</p></h3>

<p align="center">[Discord](support/discord.md)</p>

<h3><p align="center">Contribute</p></h3>

<p align="center"> [Translate](contribute/translate.md)</p>
<p align="center"> [Development](contribute/development.md)</p>

## Translations

We use Weblate to translate Wizarr, help us out by clicking [here](https://hosted.weblate.org/engage/wizarr/)

<a href="https://hosted.weblate.org/engage/wizarr/">
<img src="https://hosted.weblate.org/widgets/wizarr/-/app/multi-auto.svg" alt="Übersetzungsstatus" />

## Thank you

A big thank you ❤️ to these amazing people for contributing to this project!

<a href="https://github.com/wizarrrr/wizarr/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=wizarrrr/wizarr" />
</a>
