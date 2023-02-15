# Deploying to Heroku

- Notes:

  - This could be a sub-section in [Technical Setup][Technical Setup]
  - The [video](https://canvas.uchicago.edu/courses/41147/pages/video-deploying-to-heroku){:target="_blank"} is not yet transcribed and may change

  - Project: N/A

  - Target: N/A

  - See [Canvas](https://canvas.uchicago.edu/courses/47526/assignments/523302){:target="_blank"} for some updated instructions

  - Copied from [`deploying-to-heroku.md`](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/deploying-to-heroku.md){:target="_blank"}

### Sign in to your Heroku account (once per workspace)

 - At a terminal prompt:

    ```
    heroku login -i
    ```
 - You will see something like:

    ```
    heroku: Enter your login credentials
    Email:
    ```

 - Enter your Heroku email and password[^mfa]:
    - https://dashboard.heroku.com/account

    ```
    heroku: Enter your login credentials
    demostudent10@firstdraft.com
    Password: ***************
    Logged in as demostudent10@firstdraft.com
    ```

[^mfa]: If you have [Multi-Factor Authentication](https://devcenter.heroku.com/articles/multi-factor-authentication){:target="_blank"} enabled, then instead of your password you'll need to paste an API Key. Generate and copy your API Key under your [Account Settings in the Heroku Dashboard](https://dashboard.heroku.com/account){:target="_blank"}:

    ![](assets/deploying-to-heroku/heroku-api-key.png)

### Create a production server (once per application)

 - At a terminal prompt,

    ```
    heroku create
    ```

    This will assign a random name to your app. If you want to, you can also choose a name for the app when creating it:

    ```
    heroku create my-cool-app
    ```

    Or, at any time, you can rename the app:

    ```
    heroku rename my-awesome-app
    ```

### Change the stack

We need to select the Heroku 20 stack for the versions of Ruby/Rails we're using:

```
heroku stack:set heroku-20
```

### Deploying code to your production server

 - Make a git commit with your latest work that you wish to deploy. You can use the web interface at **/git**, or you can run the following commands at a terminal prompt:

    ```
    git add -A
    git commit -m "Describe your changes"
    ```
 - At a terminal prompt,

    ```
    git push heroku HEAD:main -f
    ```
 - That's it! Your app will be available, once deployed, at `https://my-awesome-app.herokuapp.com` (or whatever name you chose or were assigned).
 - Repeat the two steps above as many times as you like to deploy new changes.

### Set environment variables

If you need to set any environment variables on Heroku to mirror [the ones you have locally](https://chapters.firstdraft.com/chapters/792) (to e.g. store credentials securely), you can do it in [the application's settings in your Heroku dashboard](https://devcenter.heroku.com/articles/config-vars#using-the-heroku-dashboard){:target="_blank"}. (Heroku refers to environment variables as "Config Vars".)

### Optional: set a custom domain

 - To put your app behind a custom domain name, you must first verify your identity by adding a credit card to your Heroku account. This will also lift your app limit from 5 to 100.
 - Then, at a terminal prompt:

    ```
    heroku domains:add www.your-domain.com
    ```
   
 - You will see some instructions:

    ```
    heroku domains:add www.your-domain.com
    Adding test.appdevproject.com to ⬢ my-awesome-app... done
    Configure your app's DNS provider to point to the DNS Target young-peony-foamxxrzcu9xzxd286waw6ay.herokudns.com.
    For help, see https://devcenter.heroku.com/articles/custom-domains
    
    The domain www.your-domain.com has been enqueued for addition
    Run heroku domains:wait 'www.your-domain.com' to wait for completion
    ```

 - Back in your domain registrar, find the place to add "CNAME Records". Depending on the registrar, you will usually under "DNS Settings".
 - Create a CNAME record that points `www` to the target that Heroku gave you (in the example above, `young-peony-foamxxrzcu9xzxd286waw6ay.herokudns.com`).
 - That's it! It usually takes a few minutes to take effect.

### Seeing error messages

When your users run into errors, we don't want them to see the gory details of what went wrong. So, rather then show them the detailed error messages, we just show them a generic "Something went wrong" page when running the application in production mode.

But then, how will you debug errors that your users will, inevitably, discover in your code? Eventually, you should add a service like [Rollbar](https://rollbar.com/), which will automatically log every error and send you a detailed report. But for now, you should look at the error message in your server log.

How can you look at your Heroku server log? With this command:

```
heroku logs --tail
```

That will show us what's going over there in California:

**BENP: missing image, not in assets. See source**

![](assets/deploying-to-heroku/heroku log.png)

You'll notice that the production server log is not as helpful as the development log! What I do is clear the Terminal with <kbd>Cmd</kbd>+<kbd>K</kbd>, and then refresh the request that was causing the error. I then scroll to the top of the mess, and start to look through carefully for the error message.

### Running rake tasks automatically

You can run rake tasks on a schedule very easily on Heroku. First,

```
heroku addons:create scheduler:standard
```

Then,

```
heroku addons:open scheduler
```

It will give you a URL to open, at which you'll find a dashboard. You can then specify a task (e.g. `rails send_sms` or whatever you named your task) and a frequency that you want the task to be run. Your options are every day, every hour, and every 10 minutes. That's it!

