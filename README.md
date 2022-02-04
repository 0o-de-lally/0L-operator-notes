# operator-notes

## If using Google Cloud
1. Log into GCP google console, and go to Compute Engine > VM instances

You will see a list of instances.

2. Press “SSH” button for the instance of the validator.

You will then get a black terminal window.

3. In the terminal change to the “node” user on that machine.
> sudo su node

You are now executing commands as ‘node’

4. Enter Tmux
This is the terminal multiplexer where you have multiple windows with the validator’s services running.

Do whatever node maintenance is required.
