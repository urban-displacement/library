# Setting up `rclone` on the udp server

1. Log into an account via terminal on your laptop
    * `ssh udp@fargo.berkeley.edu`
2. `rclone config`
3. Use default options till you are asked for the `Option box_sub_type` and choose enterprise (option 2 as of writing this)
4. When asked for web browser authentication, say no
5. Open a new terminal on your laptop and type `rclone authorize "box"` to authorize, you'll copy over credentials on the server. Choose sso login and choose the account you want to authorize.

# Set up Google Drive API

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

ls, lsd, tree

# copy

`rclone copy gd_udp:CCI\ Docs/Admin box_udp:CCI\ Docs/Admin`

This will create a new folder `Admin` in box if it's not there already