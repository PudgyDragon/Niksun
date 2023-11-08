# Lost Access to Web UI
Quick little guide for getting into the Web UI if you know a previous password and can't get in. I found this really helpful document online. I will try to copy/paste the contents of the document into another file in the event the document is ever taken offline.
- https://www.niap-ccevs.org/MMO/Product/st_vid11204-agd.pdf


Please note, I will be using a fake RSA account for the purposes of this guide. 

## Uh-oh
You try to login to Niksun and realize your password isn't working, or your RADIUS isn't working. If you are lucky enough to still remember a previous password (with RADIUS, typically the password you set the account up with) you can change your password in CLI.

### Login to root
Based on Niksun default information, you'll need to login to `vcr` and then `su` to root (replace user/pass where needed). You can use putty, or good ole ssh:
```
ssh vcr@<IP_Address>
vcr/niksun2k13!
su/niksun2k13!
```
### Enumerate Users
Once you're logged in as root, you can enumerate all Web UI users running the following command:
```
manage_pass all
```
The output will be similar to this:
```
Enable 'user' account, status: Success
Enable 'admin' account, status: Success
Enable 'pudgy.dragon-rsa' account, status: Success
```
### Change Your Password
Even if your account is set up to user RADIUS with RSA, you can change the original password your account was set up with to a new password you're able to login with. You can do so using the following command:
```
manage_pass edit pudgy.dragon-rsa
```
This will prompt you to enter your old password, enter a new password, and verify your new password.
```
Old password for pudgy.dragon-rsa:
New password for pudgy.dragon-rsa:
Retype password for pudgy.dragon-rsa:
```
There are a couple possible outcomes. If you have the wrong password, you'll get:
```
Account 'pudgy.dragon-rsa' update, status: Incorrect old password
```
If you do have the right password which happens to be your current password, and enter the same password for your new password, you'll get:
```
Account 'pudgy.dragon-rsa' update, status: [Password cannot be the same as your current password.]
```
At the end of the day, what you're hoping for is:
```
Account 'pudgy.dragon-rsa' updated, status: Success
```
You will now be able to login to the Niksun Web UI with your fresh password.
