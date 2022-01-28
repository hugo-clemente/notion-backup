# Notion Backup

A simple GitHub repository template you can use to automate Notion backups using GitHub actions. The backups are stored on the repo, so you can keep track of them.

## Acknowledgements
Huge thanks to *Artur Burtsev* ! They're the author of the script used for the backup, and they wrote [this article](https://artur-en.medium.com/automated-notion-backups-f6af4edc298d) which is the main source of "inspiration" for this repo.

-------------------------------------------------
## How to use
Simply click the `use this template` button on GitHub to create your own repo. Next, you need to configure the secrets to get the backup script working.

### Configuring the secrets

Two things are needed : a notion access token, and a notion space ID.  

Here's how to get them in Google Chrome:

- Open http://notion.so/, go to “Settings & Members” → “Settings”
- Open Chrome DevTools by pressing Command+Option+J (Mac) or Control+Shift+J (Windows, Linux, Chrome OS)
- Go to the Network tab, as shown on a screenshot below
- Enable “XHR” filter (1), clear console (2), start the export (3), select “enqueueTask” (4)

![Drag Racing](https://miro.medium.com/max/1400/1*wVlpHE4R3LrDQxlJdhEgtg.png)

In the opened “Headers” tab you would need to scroll down until you see “cookie:” and a lot of text, in this text you need to identify a part, which looks like (5): `token_v2=xxx;` where xxx is a very long sequence of letters and digits and can span multiple lines.  
Copy everything between “token_v2=” and “;” and add it as a GitHub actions secret under the name `NOTION_TOKEN_V2` ([How to add a secret to GitHub actions](https://docs.github.com/en/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository)).
  
Now scroll to the very bottom and under the “Request Payload” section you will see something like (6): `spaceId: “4489c123-09d6-4069-ae3b-1665e25d6c03”`  
Copy the value inside quotes, and again add it as a GitHub actions secret under the name `NOTION_SPACE_ID`.

## Enabling actions

**⚠️ THIS STEP IS VERY IMPORTANT, THE BACKUP WON'T WORK IF YOU DON'T DO THIS ⚠️**

To enable the backup action, you simply need to go to the actions tab, and click `Enable actions on this repository`

-------------------------------------------------

**You should be good to go !**

The script will run everyday at 8PM UTC (configurable), and add the notion export to a `backup` folder in your repo.

## Configure the cron task
The script is run on a cron schedule. You can modify the schedule in the `.github/workflows/backup.yml` file. Look for `- cron:  '0 20 * * *'`, and change the cron schedule as desired ([use this great tool](https://crontab.guru/))

https://artur-en.medium.com/automated-notion-backups-f6af4edc298d
