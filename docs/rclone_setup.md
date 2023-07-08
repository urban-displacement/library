# Setting up
## Box.com `rclone` on the udp server

1. Log into an account via terminal on your laptop
    * `ssh udp@fargo.berkeley.edu`
2. `rclone config`
3. Use default options till you are asked for the `Option box_sub_type` and choose enterprise (option 2 as of writing this)
4. When asked for web browser authentication, say no.
    * When logged into EML on the terminal, there's no way to open a browser to authenticate. To get past this, you'll authorize through the terminal on your laptop (step 5 below). This is a kinda "fake-out" authorization to get EML to move forward.
5. Open a new terminal on your laptop (not logged into EML) and type `rclone authorize "box"` to authorize. Next, you'll copy over the provided credentials on the server side. Choose sso (Single-Sign On) login and choose the account you want to authorize.

## Set up Google Drive API

***You likely won't be using Google Drive***


[Official tutorial documentation](https://rclone.org/drive/#making-your-own-client-id)


1. Log into `https://console.cloud.google.com`
2. Create project (e.g. `gdern`)
3. Credentials > Configure Consent Screen
4. Choose internal. Name app, user support email, developer email, save
5. add scopes: full_control and read_write, then save and continue, then back to dashboard
6. Credentials, + Create Credentials, OAuth client ID
7. Select Desktop App
8. Copy client ID and Client Secret over in terminal on EML server
9. Choose (drive)
10. When asked to authorize online, choose no and do `rclone authorize "drive"` on your laptop terminal.
11. After authorizing with appropriate account on browser, copy token provided on your terminal laptop to the EML terminal account.

# Navigating with rclone

Once you've configured your rclone links, you can navigate and view directories on cloud servers like box.com. Type `rclone help` to see a bunch of options.

## Viewing available remotes

```
rclone listremotes
box_ern:
box_udp:
box_udpdata:
gd_udp:
```

## Viewing remote directories

```
rclone lsd box_ern:
rclone lsd box_ern:ERN
rclone lsd box_ern:ERN/data
```
other options include `ls` and `tree`

You can also explore a remote with a text based user interface using the arrow keys:
```
rclone ncdu box_ern:

rclone ncdu v1.62.2 - use the arrow keys to navigate, press ? for help
-- box_ern: -----------------------------------------------------------
   89.611Gi [##########] /eml_backup
   32.459Mi [          ] /ERN
    1.789Mi [          ]  Get Started with Box.pdf
   10.720Ki [          ]  quota upgrade.docx


Total usage: 89.645Gi, Objects: 5.875k

```

Press `q` to exit out of `ncdu`

# copy
## Between servers

`rclone copy gd_udp:CCI\ Docs/Admin box_udp:CCI\ Docs/Admin`

This will create a directory in box if there's not already one.

## From cloud to directory
`rclone copy box_ern:ERN/data/[some file] [path/to/directory]`


This will create a new folder `Admin` in box if it's not there already

# sync

Make source and dest identical, modifying destination only.