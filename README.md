# HomeTendr for Claude

The official Claude plugin for [HomeTendr](https://hometendr.com), the shared app for looking after a home: recurring maintenance, chores, appliances and warranties, rooms and renovations.

With the plugin, Claude works with your real HomeTendr home. See what needs doing today and tick tasks off, look up items and warranties, check the house's health, plan the week, get an autumn or spring maintenance plan, register an appliance from a receipt or type plate, and put together a handover when you sell. Claude has the same permissions as you have in the app.

## What's inside

- [`plugins/home-tendr`](plugins/home-tendr): the HomeTendr connector (`https://mcp.hometendr.com`) and four skills.
- [`.claude-plugin/marketplace.json`](.claude-plugin/marketplace.json): a marketplace with this one plugin.

## Install

In Claude Code:

```
/plugin marketplace add TinyAnvilApps/hometendr-claude-app
/plugin install home-tendr@hometendr
```

In claude.ai, add HomeTendr from the Connectors Directory. When Claude asks you to connect, sign in with your HomeTendr account (email, Apple or Google) and choose which homes to share. Owners and admins decide in the HomeTendr app (*Settings → AI → AI apps*) what AI apps may change, and you can disconnect at any time.

You need a HomeTendr account, which is free on the [App Store](https://hometendr.com). Reading works on every plan; creating and changing things needs Pro or Max.

## Support

[hometendr.com/support](https://hometendr.com/support) · [Privacy](https://hometendr.com/privacy) · [Terms](https://hometendr.com/terms)

This repository is published from HomeTendr's internal repository. Issues and pull requests here are not monitored, so please use the support page.

## License

Proprietary. See [LICENSE](LICENSE).
