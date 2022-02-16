# Heroku Deploy

**Important Notes**
1. This Branch only for deploying, generate all your private files from master branch.
2. If you want to edit aria.sh or qBittorrent.conf or any other file in bot folder you must add `UPSTREAM_REPO` of your edited public or private fork else YOU WILL GET THE OFFICIAL CODE AND ALL YOUR CHANGES WILL NOT TAKE EFFECT.
3. Use this branch to avoid suspension `OR` deploy master branch twice with same app name.
4. To stay up to date don't fill `UPSTREAM_REPO`, on each `dyno restart` you will get lastest commits from official repository or fill `UPSTREAM_REPO` by your public/private fork link and fetch manually then you can update your bot by `restart cmd` and `dyno restart`. BUT any change in requirements you need to deploy again and your bot will not boot after dyno restart, so if you have problem with this then fill `UPSTREAM_REPO`.
5. Don't delete .gitignore file.
6. Read all variables definitions from master branch readme.
7. Don't edit variables from Heroku, if you want to edit simply do it in config.env from gists if using gists or from private repository if added in it, then restart your app.
8. Keep the programmer inside you away and follow the steps.

------

<details>
<summary><b><u>With CLI</u></b></summary>

## With CLI

- Clone this repo:
```
git clone https://github.com/anasty17/mirror-leech-telegram-bot mirrorbot/ && cd mirrorbot
```
- Switch to heroku branch
  - **NOTE**: Don't commit changes in master branch. If you have committed your changes in master branch and after that you switched to heroku branch, the new added files will `NOT` appear in heroku branch.
```
git checkout heroku
```
- After adding your private data
```
git add . -f
```
- Commit your changes
```
git commit -m token
```
- Login to heroku
```
heroku login
```
- Create heroku app
```
heroku create --region us YOURAPPNAME
```
- Add remote
```
heroku git:remote -a YOURAPPNAME
```
- Create container
```
heroku stack:set container
```
- Push to heroku
```
git push heroku heroku:master -f
```

------

### Extras

- To create heroku-postgresql database
```
heroku addons:create heroku-postgresql
```
- To delete the app
```
heroku apps:destroy YOURAPPNAME
```
- To restart dyno
```
heroku restart
```
- To turn off dyno
```
heroku ps:scale web=0
```
- To turn on dyno
```
heroku ps:scale web=1
```
- To set heroku variable
```
heroku config:set VARNAME=VARTEXT
```
- To get live logs
```
heroku logs -t
```

------
</details>


## With Github Workflow

1. Go to Repository Settings -> Secrets

2. Add the below Required Variables one by one by clicking New Repository Secret every time.

   - HEROKU_EMAIL_1: Heroku Account Email Id in which the above app will be deployed
   - HEROKU_API_KEY_1: Your Heroku API key, get it from https://dashboard.heroku.com/account
   - HEROKU_APP_NAME_1: Your Heroku app name, Name Must be unique
   - CONFIG_FILE_URL_1: Copy [This](https://raw.githubusercontent.com/anasty17/mirror-leech-telegram-bot/master/config_sample.env) in any text editor.Remove the _____REMOVE_THIS_LINE_____=True line and fill the variables. For details about config you can see Here. Go to https://gist.github.com and paste your config data. Rename the file to config.env then create secret gist. Click on Raw, copy the link. This will be your CONFIG_FILE_URL.
   
   - HEROKU_EMAIL_2: Heroku Account Email Id in which the above app will be deployed
   - HEROKU_API_KEY_2: Your Heroku API key, get it from https://dashboard.heroku.com/account
   - HEROKU_APP_NAME_2: Your Heroku app name, Name Must be unique
   - CONFIG_FILE_URL_2: Copy [This](https://raw.githubusercontent.com/anasty17/mirror-leech-telegram-bot/master/config_sample.env) in any text editor.Remove the _____REMOVE_THIS_LINE_____=True line and fill the variables. For details about config you can see Here. Go to https://gist.github.com and paste your config data. Rename the file to config.env then create secret gist. Click on Raw, copy the link. This will be your CONFIG_FILE_URL.

3. Remove commit id from raw link to be able to change variables without updating the CONFIG_FILE_URL in secrets. Should be in this form: https://gist.githubusercontent.com/username/gist-id/raw/config.env
   - Before: https://gist.githubusercontent.com/anasty17/8cce4a4b4e7f4ea47e948b2d058e52ac/raw/19ba5ab5eb43016422193319f28bc3c7dfb60f25/config.env
   - After: https://gist.githubusercontent.com/anasty17/8cce4a4b4e7f4ea47e948b2d058e52ac/raw/config.env

   - You only need to restart your bot after editing config.env Gist secret.

4. After adding all the above Required Variables go to Github Actions tab in your repository.
   - Select Deploy to Heroku workflow.

5. Then click on Run workflow
