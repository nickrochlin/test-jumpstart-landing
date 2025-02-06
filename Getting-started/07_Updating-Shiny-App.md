Our Shiny Server is accessed through SSH, which requires you to be on campus or connected to UBC\'s VPN if off campus.

### VPN

If needing to connect to UBC\'s VPN, please [follow these instructions from UBC IT](https://it.ubc.ca/services/email-voice-internet/myvpn/setup-documents).

Once the Cisco client is installed, launch it and log in to `myvpn.ok.ubc.ca`

### SSH

First, we\'ll ensure you have an SSH client on your computer.

This should be available by default on a Mac, and comes packaged with Git Bash on your Windows PC. If you haven\'t installed Git on your PC yet, check out the `README` for this repo.

On a Mac open your Terminal and on a PC open Git Bash. Type SSH

```
$ ssh
```

If you get the following output, you're all good

```
usage: ssh [-46AaCfGgKkMNnqsTtVvXxYy] [-B bind_interface]
           [-b bind_address] [-c cipher_spec] [-D [bind_address:]port]
           [-E log_file] [-e escape_char] [-F configfile] [-I pkcs11]
           [-i identity_file] [-J [user@]host[:port]] [-L address]
           [-l login_name] [-m mac_spec] [-O ctl_cmd] [-o option] [-p port]
           [-Q query_option] [-R address] [-S ctl_path] [-W host:port]
           [-w local_tun[:remote_tun]] destination [command]
```

If not you\'ll need to troubleshoot. Check with Jason or Mathew about trouble shooting.

### Connect to the UBC Server

In Terminal or Git Bash type

```
$ ssh yourCWL@s226.ok.ubc.ca
```

In my case this is

```
$ ssh vdunbar@s226.ok.ubc.ca
```

The first time you do this, you may get the following message

```
The authenticity of host 's226.ok.ubc.ca (206.87.25.206)' can't be established.
ED25519 key fingerprint is SHA256:pbqRzzTNDL+fudkCPxYnH4CvtiDAwaW3P6HAgfcejro.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

That\'s okay. Say yes. Normally, and following this, you should get this

```
         Welcome to s226
         Your IP, Login Time, Username are logged.
         Unauthorized access will be reported.

yourCWL@s226.ok.ubc.ca's password:
```

Enter your CWL password (you will only see blank space, this is normal), and hit enter. That's it, you're in!

### Navigating

Type `ls` to see your directories

```
$ ls

openscience  public_html
```

Inside of `openscience` you\'ll see a directory `shiny`. This is where you will place your folder containing your `app.R`.

Now we know you can connect to the server.

### Removing an Old App

If updating an existing app, say the app for BIOL-116, we\'ll start by removing the old app after connecting to the server

```
$ rm ~/openscience/shiny/BIOL-116/app.R
```

### Copying New App to Server

End your SSH session

```
$ exit
```

And copy from your local machine with `scp`. In this case, we're assuming the app is in a folder in our home directory on our local machine called `BIOL-116` and writing into an existing directory, `BIOL-116` - note that you need to update the code below with your own CWL in two locations

```
$ scp ~/BIOL-116/app.R yourCWL@s226.ok.ubc.ca:/home/yourCWL/openscience/shiny/BIOL-116/
```

You should see

```
 Welcome to s226
         Your IP, Login Time, Username are logged.
         Unauthorized access will be reported.

yourCWL@s226.ok.ubc.ca's password:
```

Enter your password, and hopefully success!

```
app.R                                         100%   24KB 608.7KB/s   00:00
```

## Testing the App

A number of things may go wrong when trying to launch the app from the server; when doing so from the app's url, you will not get a very informative error message.

Three of the more likely things to go awry are that you have used an `R` package that is not installed on the server, you have used an `R` package that requires a system library that has not been installed on the server's operating system, or that your file permissions are not allowing the server to access needed files.

Each of these can be easily identified by launching the app directly from the server and reading the error message. `ssh` onto the server and run the following to launch the app:

```
R -e "shiny::runApp('~/openscience/shiny/BIOL-116')"
```

## Restarting the Server

```
sudo systemctl restart shiny-server
```

## Checking the logs

Should you want to go dumpster diving into logs and other bits (be careful, this makes you root, which is potentially dangerous):

```
sudo su

cd /var/log

tail | cat | grep  # whatever logs you want to look at, /var/log/shiny-server contains more logs
```
