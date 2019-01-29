<p align="center">
    <img src="https://github.com/Zilliqa/Zilliqa/blob/master/img/zilliqa-logo-color.png" width="200" height="200">
</p>

<p align="center">Zilliqa JSON-RPC API documentation. Powered by Slate.</p>

## Overview

Zilliqa apidocs contains the documentation of JSON-RPC methods used to interact with Zilliqa nodes in order to transact and deploy/call contracts. You may currently find support for following all languages:

* cURL
* [Javascript](https://github.com/Zilliqa/Zilliqa-JavaScript-Library)

## Prerequisites

You're going to need the following to contribute:

* **Linux or macOS** — Windows may work, but is unsupported.
* **Ruby, version 2.3.1 or newer**
* **Bundler** — If Ruby is already installed, but the `bundle` command doesn't work, just run `gem install bundler` in a terminal.

## Contributing to Zilliqa apidocs

1. Fork this repository on GitHub.
2. Clone *your forked repository* (not our original one) to your hard drive with
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

Learn more about editing Slate markdown [**HERE**](https://github.com/lord/slate/wiki/Markdown-Syntax).

Please adhere to the [Code of Conduct](./CODE_OF_CONDUCT.md) when participating in the Zilliqa community.
