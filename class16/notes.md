Open an SSH client.
Locate your private key file. The key used to launch this instance is keymaria.pem
Run this command, if necessary, to ensure your key is not publicly viewable.
chmod 400 ~/Downloads/keymaria.pem
Connect to your instance using its Public DNS:
ec2-52-89-94-158.us-west-2.compute.amazonaws.com
Example:
ssh -i ~/Downloads/keymaria.pem ubuntu@ec2-52-89-94-158.us-west-2.compute.amazonaws.com