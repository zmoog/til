# Backup an Obsidian vault to a GitHub repo

I leverage iCloud Drive to sync my Obsidian vaults between my Mac, iPhone, and iPad. Unfortunately, iCloud Drive doesn't offer you the following:

- sync status
- sync activity
- file version history
- file restore capabilities

When Apple introduced iCloud Drive, the service was flaky for a while, but in recent years has grown a lot, and now it syncs pretty reliably. Still, the lack of the features mentioned above makes me anxious as my vault's size increases over time.

Will I recover a file deleted by mistake or resolve conflicting edits on different devices? I'm not 100% sure.

So I decided to add an offsite backup solution: periodically commit vault files changed on my laptop and push them to a private GitHub repo.


## Create a private GitHub repository

```shell
# Create a brand new private repository to host the files from the vault
$ gh repo create zmoog/obsidian-vault-maintenance --private
✓ Created repository zmoog/obsidian-vault-maintenance on GitHub

# Walk into the vault directory
cd /Users/${USER}/Library/Mobile\ Documents/iCloud~md~obsidian/Documents/Maintenance

# Initialize a new Git repository
git init

# Set the GitHub repository as remote
git remote add origin git@github.com:zmoog/obsidian-vault-maintenance.git

# set git options (they apply to this repository only)
git config user.name "Automated"
git config user.email "actions@users.noreply.github.com"
    
# add everything changed to the stage
git add -A

# create the initial commit
git commit -m "Latest data: ${timestamp}"

# push and set the GitHub repository as upstream
git push -u origin main
```

## Create a sync script

```shell
#!/bin/bash

# make the script exit immediately if a command returns a non-zero exit status
set -e

# list of Obsidian vaults we want to sync
vaults=("Elastic" "Knowledge")

for vault in ${vaults[@]}
do
    # walk into the vault directory
    cd /Users/${USER}/Library/Mobile\ Documents/iCloud~md~obsidian/Documents/${vault}

    # TODO: check this is a Git repository
    #

    # set git options for this repository only
    git config user.name "Automated"
    git config user.email "actions@users.noreply.github.com"
    
    # add everything changed to the stage
    git add -A

    # commit everything changed
    timestamp=$(date -u)
    git commit -m "Latest data: ${timestamp}" || continue

    # push the commit to the remote repo
    git push    
done
```

## Schedule the sync every few hours

Open cron

```shell
crontab -e
```

Schedule the script execution every four hours:

```shell
0 */4 * * * /Users/zmoog/bin/sync-obsidian.sh
```

