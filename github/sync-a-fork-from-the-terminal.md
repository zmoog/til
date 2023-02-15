# Sync a fork from the terminal

Sometimes your are working on a fork and you need to sync it with the upstream repo before starting a new task.

The GitHub CLI offers a quick and easy way to archieve this!

```shell

$ gh repo sync zmoog/integrations -b main                                                                                                                         main  ✭ ✱
✓ Synced the "zmoog:main" branch from "elastic:main"

```

After a few seconds, my fork of elastic/integrations repo is up to date and ready for a `git pull`.
