<p align="center">
    <a href="https://github.com/Zilliqa/Zilliqa" target="_blank"><img src="https://github.com/Zilliqa/Zilliqa/blob/master/img/zilliqa-logo-color.png" width="200" height="200"></a>
</p>

<p align="center"><b>Zilliqa JSON-RPC API documentation. Powered by <a href="https://github.com/lord/slate" target="_blank">Slate</a>.</b></p>
<p align="center"><a href="https://discord.gg/XMRE9tt" target="_blank"><img src="https://img.shields.io/discord/370992535725932544.svg" /></a></p>

## Overview

Zilliqa apidocs contains the documentation of all JSON-RPC methods used to interact with Zilliqa nodes in order to transact and deploy/call contracts. You may currently find support for:

- cURL
- JavaScript via [`zilliqa-js`](https://github.com/Zilliqa/Zilliqa-JavaScript-Library)
- Java via [`laksa-j`](https://github.com/FireStack-Lab/LaksaJ)
- Ruby via [`laksa-ruby`](https://github.com/FireStack-Lab/LaksaRuby)
- Go via [`gozilliqa-sdk`](https://github.com/Zilliqa/gozilliqa-sdk.git)

## Contributing to Zilliqa apidocs

### Prerequisites

You're going to need the following to contribute:

- **Linux or macOS** — Windows may work, but is unsupported.
- **Ruby, version 2.3.1 or newer**
- **Bundler** — If Ruby is already installed, but the `bundle` command doesn't work, just run `gem install bundler` in a terminal.

### Running apidocs locally

1. Fork this repository on GitHub.
2. Clone _your forked repository_ (not our original one) to your hard drive with
   ```shell
   git clone https://github.com/Zilliqa/apidocs.git && cd apidocs
   ```
3. Initialize and start Slate. You can either do this locally, or with Vagrant:

   ```shell
   # either run this to run locally
   bundle install
   bundle exec middleman server

   # OR run this to run with vagrant
   vagrant up
   ```

You can now see the docs at http://localhost:4567.

### Contributing guidelines

- Learn more about editing Slate markdown [**HERE**](https://github.com/lord/slate/wiki/Markdown-Syntax).
- Please adhere to the [**Code of Conduct**](./CODE_OF_CONDUCT.md) when participating in the Zilliqa community.
- Please utilise the [**PR template**](./.github/PULL_REQUEST_TEMPLATE.md) when submitting Pull Requests to this repository.
