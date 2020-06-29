# PaperMC/Paper Heroku buildpack

## Run your Paper minecraft server on the cloud with Heroku.

This is a Heroku [buildpack](https://devcenter.heroku.com/articles/buildpacks).

## Requirements

1. A free Heroku account. [Sign up here](https://signup.heroku.com)

2. A ngrok account (for ip tunneling). [Sign up here](https://ngrok.com/signup)

3. A dropbox account for files sync. [Sign up here](https://www.dropbox.com/login) (info below)

## Usage

After downloading and installing the Heroku CLI, open Command Prompt (cmd) and type

```
heroku login
```

Next, simply copy the following lines to your Command Promt (cmd)

```
heroku create
heroku buildpacks:add heroku/jvm
heroku buildpacks:add https://github.com/leothecoolest/PaperMC-Heroku-Buildpack
heroku ps:exec
git commit -m "Heroku Exec" --allow-empty
done
```

Then, manually add these configs with your NGROK auth token and Dropbox API token

```
$ heroku config:set NGROK_API_TOKEN="xxxxx"
$ heroku config:set DBCONFIG="xxxxx"
```

Then copy these commands in the cmd

```
git push heroku master
heroku ps:scale web=1
```

And you're done!

Go [here](https://dashboard.ngrok.com/status/tunnels) or your Heroku app domain to check your server ip.

## Customizing Minecraft

You can choose the Minecraft version by setting the MINECRAFT_VERSION like so:

The Minecraft versions are listed at the [PaperMC](https://papermc.io/downloads#Paper) offical site.

```
heroku config:set MINECRAFT_VERSION="1.8.9"
```

You can also configure the server properties by creating a server.properties file in your project and adding it to Git. This is how you would set things like Creative mode and Hardcore difficulty. The various options available are described on the Minecraft Wiki.

You can add files such as ``banned-players.json``, ``banned-ips.json``, ``ops.json``, ``whitelist.json`` to your Git repository and the Minecraft server will pick them up.

## Tips

You can create your own server on your computer with your own plugins, worlds then ZIP it to a file with the name **backup.zip**. Upload it to dropbox and you will have your own configured server.
