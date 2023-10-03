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
<BR>
<h1><p align="center">Table of contents
<br>Welcome to the Wizarr Documentation</p></h1>

<h3><p align="center">💾 Getting-Started</p></h3>
<a id="docker"></a>
<h3><p align="center">[Installation]
  <p align="center">
    
<a id="docker"></a>
<h3><p align="center">[Docker]
  <p align="center">
    
<a id="unraid"></a>
<h3><p align="center">[unRAID]
  <p align="center">

<h3><p align="center"><a class="heading-link" href="#-using-wizarr-1">💭 Using Wizarr</p></h3>

# Introduction

<p align="center">Wizarr is a automatic user invitation system for Plex, Jellyfin and Emby.</p>
  <p align="center">Create a unique link and share it to a user and they will automatically be invited to your media Server!</p>
    <p align="center">They will even be guided to download the client and instructions on how to use your requests software!</p>

### Features

* Automatic Invitation to your Media Server (Plex, Jellyfin, Emby...)
* Secured invitation environment
* Plug and Play SSO Support\*
* Multi-tiered Invitations
* Duration for membership
* Guide user on how to download Plex client
* Requests Integration: Guide users on how to request Movie (Jellyseerr, Overseerr & Ombi)
* Discord Server Integration: Invite users to your Discord Server
* Customizable: Add any Custom HTML

<BR><BR>
# 💾 Getting-Started

### Docker <p align="center"><img src="https://1000logos.net/wp-content/uploads/2021/11/Docker-Logo.png" height="200"></p>

{% hint style="warning" %}
Be sure to replace`/path/to/appdata/config` in the below examples with a valid host directory path. If this volume mount is not configured correctly, your Wizarr settings/data will not be persisted when the container is recreated (e.g., when updating the image or rebooting your machine).

The `TZ` environment variable value should also be set to the [TZ database name](https://en.wikipedia.org/wiki/List\_of\_tz\_database\_time\_zones) of your time zone!
{% endhint %}

{% tabs %}
{% tab title="Docker Compose (recommended)" %}


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


<BR>
### unRAID <p align="center"><img src="https://craftassets.unraid.net/uploads/logos/unraid-stacked-dark.svg" height="100"></p>

1. Ensure you have the **Community Applications** plugin installed.
2. Inside the **Community Applications** app store, search for **Wizarr**.
3. Click the **Install Button**.
4. On the following **Add Container** screen, make changes to the **Host Port** and **Host Path 1**(Appdata) as needed, as well as the environment variables.
5. Click apply and access "Wizarr" at your `<ServerIP:HostPort>` in a web browser.
</p>



<BR><BR><BR>
# Reverse Proxy

## Nginx
---
<p align="center"><img src="https://www.svgrepo.com/show/373924/nginx.svg" height="100"></p>

{% tabs %}
{% tab title="SWAG" %}
Create a new file `wizarr.subdomain.conf` in `proxy-confs` with the following configuration:

```nginx
server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;

    server_name wizarr.*;

    include /config/nginx/ssl.conf;

    client_max_body_size 0;

    location / {
        include /config/nginx/proxy.conf;
        resolver 127.0.0.11 valid=30s;
        set $upstream_app wizarr;
        set $upstream_port 5690;
        set $upstream_proto http;
        proxy_pass $upstream_proto://$upstream_app:$upstream_port;
    }

}
```
{% endtab %}

{% tab title="Nginx Proxy Manager" %}
Add a new proxy host with the following settings:

#### Details

* **Domain Names:** Your desired external wizarr hostname; e.g., `wizarr.example.com`
* **Scheme:** `http`
* **Forward Hostname / IP:** Internal wizarr hostname or IP
* **Forward Port:** `5690`
* **Cache Assets:** yes
* **Block Common Exploits:** no 

#### SSL

* **SSL Certificate:** Select one of the options; if you are not sure, pick “Request a new SSL Certificate”
* **Force SSL:** yes
* **HTTP/2 Support:** yes
{% endtab %}

{% tab title="Subdomain" %}
Add the following configuration to a new file `/etc/nginx/sites-available/wizarr.example.com.conf`:

```nginx
server {
    listen 80;
    server_name wizarr.example.com;
    return 301 https://$server_name$request_uri;
}

server {
    listen 443 ssl http2;
    server_name wizarr.example.com;

    ssl_certificate /etc/letsencrypt/live/wizarr.example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/wizarr.example.com/privkey.pem;

    proxy_set_header Referer $http_referer;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Real-Port $remote_port;
    proxy_set_header X-Forwarded-Host $host:$remote_port;
    proxy_set_header X-Forwarded-Server $host;
    proxy_set_header X-Forwarded-Port $remote_port;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_set_header X-Forwarded-Ssl on;

    location / {
        proxy_pass http://127.0.0.1:5690;
    }
}
```

Then, create a symlink to `/etc/nginx/sites-enabled`:

```bash
sudo ln -s /etc/nginx/sites-available/wizarr.example.com.conf /etc/nginx/sites-enabled/wizarr.example.com.conf
```
{% endtab %}
{% endtabs %}

## Traefik (v2) <p align="center"> <img src="https://www.suse.com/c/wp-content/uploads/2021/09/rancher_blog_traefik.logo_.png" height="125">

Add the following labels to the wizarr service in your `docker-compose.yml` file:

```
labels:
  - "traefik.enable=true"
  ## HTTP Routers
  - "traefik.http.routers.wizarr-rtr.entrypoints=https"
  - "traefik.http.routers.wizarr-rtr.rule=Host(`wizarr.domain.com`)"
  - "traefik.http.routers.wizarr-rtr.tls=true"
  ## HTTP Services
  - "traefik.http.routers.wizarr-rtr.service=wizarr-svc"
  - "traefik.http.services.wizarr-svc.loadbalancer.server.port=5690"
```

For more information, please refer to the [Traefik documentation](https://doc.traefik.io/traefik/user-guides/docker-compose/basic-example/).

## Caddy <p align="center"><img src="https://dqah5woojdp50.cloudfront.net/original/2X/5/5f2c1a30bf4aeec78ece52d64426ec606d9fee7d.png" height="75"></p>

{% tabs %}
{% tab title="Subdomain" %}
Add the following site block to your Caddyfile:

```
wizarr.example.com {
    reverse_proxy http://127.0.0.1:5690
}
```
{% endtab %}

{% tab title="Path" %}
You need the [response replacement](https://github.com/caddyserver/replace-response) module to use this config.

Add the following site block to your Caddyfile:

```
plex.example.com {
    redir /wizarr /wizarr/admin

    handle_path /wizarr/* {
        replace {
            "href=\"/"      "href=\"/wizarr/"
            "action=\"/"    "action=\"/wizarr/"
            "\"/static"       "\"/wizarr/static"
            "hx-post=\"/"   "hx-post=\"/wizarr/"
            "hx-get=\"/"    "hx-get=\"/wizarr/"
            "scan=\"/"      "href=\"/wizarr/"
            "/scan"         "/wizarr/scan"
            # include in join code path copy
            "navigator.clipboard.writeText(url + \"/j/\" + invite_code);" "navigator.clipboard.writeText(url + \"/wizarr/j/\" + invite_code);"
        }
        
        # Your wizarr backend
        reverse_proxy http://127.0.0.1:5690
    }
    # Your main service that you want at /
    reverse_proxy http://127.0.0.1:5055
}
```


{% endtab %}
{% endtabs %}</p>

<h1><p align="center" class="heading-link" href="#-using-wizarr-1">💭 Using Wizarr</p></h1>

#### **Wizarr supports SSO via disabling its inbuilt authentication**
<p align="center"><img src="https://www.mindcentric.com/hubfs/SingleSignOn.png" height="100"></p>

To Disable Wizarr's inbuilt authentication in order to put it behind a Proxy Provider (Authelia, Authentik...), set the following variable:

`DISABLE_BUILTIN_AUTH=True`

#### Whitelist Public Paths (important!)

In order to make the invitation process available for non signed in users, make sure you whitelist the following paths:

{% tabs %}
{% tab title="Authelia" %}
```
    - domain: wizarr.domain.com
      resources:
        - '^/j/'
        - '^/join/'
        - '^/setup/*'
        - '^/static/'
      policy: bypass
```
{% endtab %}

{% tab title="Authentik/Other" %}
```
- '^/j/'
- '^/join/'
- '^/setup/*'
- '^/static/'
```
{% endtab %}
{% endtabs %}
</p>

### Discord
<p align="center"><img src="https://assets-global.website-files.com/6257adef93867e50d84d30e2/636e0b5061df29d55a92d945_full_logo_blurple_RGB.svg" height="100"></p>
<h3><p align="center">Discord Integration</p></h3>

Please use the ```ghcr.io/wizarrrr/wizarr:dev``` docker image to use these features.

**Jellyseerr**

1. Go to your Jellyseerr settings and copy the API key.
2. Go to your Wizarr settings and select Jellyseerr from the dropdown.
3. Input your Jellyseerr base URL.
4. Input your Jellyseerr API key.

**Overseerr**

1. Go to your Overseerr settings and copy the API key.
2. Go to your Wizarr settings and select Overseerr from the dropdown.
3. Input your Overseerr base URL.
4. Input your Overseerr API key.

**Ombi**

1. Go to your Ombi settings, then click "Configuration" and select "General" from the dropdown.
2. Copy the API key from the "API Key" field.
3. Go to your Wizarr settings and select Ombi from the dropdown.
4. Input your Ombi base URL.
5. Input your Ombi API key.

### Usage

Now when a user is invited to your media server, they will be automatically added to your request software. They will also be guided on how to request Movies and TV Shows. When a user expires or is deleted from Wizarr, they will also be removed from your request software.
</p>
<p align="center">* [Discord Integration]
# Discord Integration

#### Find your Discord Server ID

1. In Discord, go to your **Server Settings**
2. Select the **Widget** tab
3. Enable Server Widget
4. Choose an Invite Channel (`general` for example)
5. Copy your **Server ID**

#### Toggle the Discord Widget

Wizarr supports using either the standard Discord widget, or a custom widget utilizing the Discord API. The custom widget is enabled by default, and provides a more integrated look and feel, however if this is not desired you can toggle the standard widget on in Wizarr's settings.

{% tabs %}
{% tab title="Custom Widget" %}
<figure><img src="../.gitbook/assets/custom-widget.png" alt=""><figcaption><p>Custom Discord Widget</p></figcaption></figure>
{% endtab %}

{% tab title="Standard Widget" %}
<figure><img src="../.gitbook/assets/default-widget.png" alt=""><figcaption><p>Standard Discord Widget</p></figcaption></figure>
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**Why not use an invitation link?**

Enabling the widget and the invite channel makes the Discord API dynamically generate an invitation link for the purpose of the widget.

This means that to use this integration, you don't need to generate a Never expiring invitation, which some users might want to avoid.
{% endhint %}
</p>

# ⛑ Support
Join our discord server
<p align="center">https://discord.com/invite/wsSTsHGsqu</p>

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

<p align="center">[Conclusion](#conclusion)</p>
