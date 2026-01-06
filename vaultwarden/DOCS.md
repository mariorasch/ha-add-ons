# Vaultwarden - password management add-on for Home Assistant

This community add-on for Home Assistant allows you to use [Vaultwarden](https://github.com/dani-garcia/vaultwarden), a lightweight and open-source server implementation of the Bitwarden Client API that is optimized for self-hosting.

Bitwarden is an open-source password manager that can store sensitive information such as website credentials in an end-to-end encrypted vault.

The Bitwarden platform offers a variety of client applications including a web interface, desktop applications, browser extensions and mobile apps.

## Installation

The installation of this add-on is pretty straightforward and not different in comparison to installing any other Home Assistant add-on.

1. Click the Home Assistant My button below to open the add-on on your Home Assistant instance.

   [![Open this add-on in your Home Assistant instance.][addon-badge]][addon]

1. Click the "Install" button to install the add-on.
1. Start the "Vaultwarden" add-on.
1. Check the logs of the "Vaultwarden" add-on to see if everything went well and to get the admin token.
1. Click the "Open Web UI" button to open Vaultwarden.
1. Add `/admin` to the URL to access the admin panel, e.g., `http://homeassistant.local:7277/admin`. Log in using the admin token you got in step 4.
1. The admin token in the logs is only shown until it is saved or changed. Hit save in the admin panel to use the randomly generated token or change it to one of your choosing.
1. Be sure to store your admin token somewhere safe. **The add-on will never show it again!**

## Configuration

**Note**: _Remember to restart the add-on when the configuration is changed._

Example add-on configuration:

```yaml
log_level: info
ssl: false
request_size_limit: 10485760
```

**Note**: _This is just an example, don't copy and paste it! Create your own!_

### Option: `log_level`

The `log_level` option controls the level of log output by the addon and can be changed to be more or less verbose, which might be useful when you are dealing with an unknown issue. Possible values are:

- `trace`: Show every detail, like all called internal functions.
- `debug`: Shows detailed debug information.
- `info`: Normal (usually) interesting events.
- `warning`: Exceptional occurrences that are not errors.
- `error`: Runtime errors that do not require immediate action.
- `fatal`: Something went terribly wrong. Add-on becomes unusable.

Please note that each level automatically includes log messages from a more severe level, e.g., `debug` also shows `info` messages. By default, the `log_level` is set to `info`, which is the recommended setting unless you are troubleshooting.

### Option: `ssl`

Enables / disables SSL (HTTPS). Set it `true` to enable it, `false` otherwise.

**Note**: _The SSL settings only apply to direct access and has no effect on the Ingress service._

### Option: `certfile`

The certificate file to use for SSL.

**Note**: _The file MUST be stored in `/ssl/`, which is the default_

### Option: `keyfile`

The private key file to use for SSL.

**Note**: _The file MUST be stored in `/ssl/`, which is the default_

### Option: `request_size_limit`

By default the API calls are limited to 10MB. This should be sufficient for most cases, however if you want to support large imports, this might be limiting you. On the other hand you might want to limit the request size to something smaller than that to prevent API abuse and possible DOS attack, especially if running with limited resources.

To set the limit, you can use this setting: 10MB would be `10485760`.

## Known issues and limitations

- Some web browsers, like Chrome, disallow the use of Web Crypto APIs in insecure contexts. In this case, you might get an error like `Cannot read property 'importKey'`. To solve this problem, you need to enable SSL and access the web interface using HTTPS.

## License

MIT License

Copyright (c) 2019-2025 Franck Nijhof

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

[addon-badge]: https://my.home-assistant.io/badges/supervisor_addon.svg
[addon]: https://my.home-assistant.io/redirect/supervisor_addon/?addon=e0afc296_vaultwarden&repository_url=https%3A%2F%2Fgithub.com%2Fmariorasch%2Fha-add-ons%2Frepository
