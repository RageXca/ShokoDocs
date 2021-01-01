+++
title = "ShokoMetadata - Linux Installation"
lastMod = 2020-04-09

[[pageNav]]
navTitle = "Folder Setup"
name = "Setting up Folders"
id = "setting-up-folders"

markup = "mmark"
+++

Credits to igloo4#9768 on Discord for the [initial write up](https://pastebin.com/urr37buE)

## Is Shoko Server Mandatory?

The short answer is **Yes**.

Shoko Server is the back-end of the entire Shoko suite, which means every single program and plugin provided uses it for accessing and maintaining your anime collection. This makes Shoko Server **mandatory** and also means Shoko Server **must be running** to use any of the programs or plugins that connect to it. With the exception of file importing, Shoko Server is no more resource intensive than other programs you probably have running in the background so you don't need to worry about Shoko Server eating up resources.

## Note about folders

For the sake of simplicity, it's assumed that the Data folder for Plex Media Server is found at
>/var/lib/plex/Plex Media Server/
and all steps are executed by the user running the Plex Media Server (usually called **plex**) in a shell (e.g. Bash)

Please adjust your paths accordingly where necessary.

## Setting up Folders

Go to the Plug-ins Directory
>cd /var/lib/plex/Plex Media Server/Plug-ins/

Download latest master build
>wget https://github.com/Cazzar/ShokoMetadata.bundle/archive/master.zip

Extract the downloaded archive/master
>unzip master.zip

Delete the archive
>rm master.zip

Rename the folder created by extraction
>mv ShokoMetadata.bundle-master ShokoMetadata.bundle

Create Scanners directory if not existing
>mkdir -p /var/lib/plex/Plex Media Server/Scanners

copy Scanner files
>cp -R ShokoMetadata.bundle/Contents/Resources/\* ../Scanners/

If you are hosting shoko on a different Machine, are using a different user than "**Default**"  or set a **password**,
you'll have to edit
>/var/lib/plex/Plex Media Server/Scanners/Movies/Shoko Movie Scanner.py
and
>/var/lib/plex/Plex Media Server/Scanners/Series/Shoko Series Scanner.py

change the following fields as necessary
~~~
Prefs = {
    'Hostname': '127.0.0.1',
    'Port': 8111,
    'Username': 'Default',
    'Password': '',
    'IncludeOther': True
}
~~~

And that concludes the installation.

## Ubuntu 20.04.1 Quick Setup copy'n'paste
This assume you are not connected as a "plex" user which is why the chown/chmod at the end.
First the path ( Based on Ubuntu Headless server 20.04.1 )
>cd /var/lib/plexmediaserver/Library/Application Support/Plex Media Server/Plug-ins

Getting the files
>sudo wget https://github.com/Cazzar/ShokoMetadata.bundle/archive/master.zip

Unziping the removing and renaming
>sudo unzip master.zip

>sudo rm master.zip

>sudo mv ShokoMetadata.bundle-master ShokoMetadata.bundle

If you never installed a Plex scanner previously you need to make the folder
>sudo mkdir -p '/var/lib/plexmediaserver/Library/Application Support/Plex Media Server/Scanners'

Since we are already in the plugin folder lets copy certain files
>sudo cp -R ShokoMetadata.bundle/Contents/Resources/* ../Scanners/

If shoko server is on a different machine or you are not using 'Default' user enter login password by editing those two files
>sudo pico '/var/lib/plexmediaserver/Library/Application Support/Plex Media Server/Scanners/Movies/Shoko Movie Scanner.py'

>sudo pico '/var/lib/plexmediaserver/Library/Application Support/Plex Media Server/Scanners/Series/Shoko Series Scanner.py'

Chmod and Chown both
>sudo chown -R plex:plex '/var/lib/plexmediaserver/Library/Application Support/Plex Media Server/Plug-ins/'

>sudo chmod 775 -R '/var/lib/plexmediaserver/Library/Application Support/Plex Media Server/Plug-ins/'

>sudo chown -R plex:plex '/var/lib/plexmediaserver/Library/Application Support/Plex Media Server/Scanners'

>sudo chmod -R 775 '/var/lib/plexmediaserver/Library/Application Support/Plex Media Server/Scanners'

Thats it.
