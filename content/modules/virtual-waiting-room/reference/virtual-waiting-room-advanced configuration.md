---
title: Virtual Waiting Room Advanced Configuration
description: Settings Available for the Virtual Waiting Room module
keywords: Section, training, virtual waiting room, platform overview
weight: 1
---



## Virtual Waiting Module Settings

Once your application has been set up with Virtual Waiting Room you will find the following files under `Advanced Config > virtualwaitingroom` in the Section Console.

### `virtualwaitingroom.json`



`virtualwaitingroom.json` will contain the configuration of your virtual waiting room and should have the following data.



{{< gist section-io-gists 23679bef63d4f455c23f599a23a362fa >}}


The settings are as follows :


- `"api_key" : "<YourGoSquaredAPIKey>"`

This will be provided by the Sectin support team.

- `"threshold" : 1000`

Threshold is the max number of concurrent customers you want on your site.


- `"enabled" : true/false`

You can enable/disable image optimization by changing the value for the "enabled" option. When in a disabled state the module acts as a reverse proxy.

- `"section_visitors_version" : "1"`

Updating this value will force the user to go through the virtual waiting room check even if they are active on the site. This can be useful for forcing active traffic off the site in times of extreme load.

- `"hostname" : "<YourHostname>"`

This is the first hostname(domain name) used in your Section Application.

### `waiting-room.html`

`waiting-room.html` will contain the HTML to be displayed in case the number of concurrent users on the site is more than the threshold set by you. Any CSS required to style the page should be included in this HTML file itself. Any images you wish to serve should be stored off domain (for e.g. in an S3 bucket) and then linked.

{{< gist section-io-gists bd435ecb59e11183c6e689af629b1a63 >}}