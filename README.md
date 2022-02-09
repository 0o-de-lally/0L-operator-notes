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

> tmux a

You should see your running services.

5. Do whatever node maintenance is required.

# Tmux Tips

To execute tmux functions, you'll need to use some keystrokes.

All commands start with a keystroke prefix of "ctrl+b".

1. Exit tmux without stopping any apps: `ctrl+b` then `d`
1. Change tmux pane: "ctrl+b" then an arrow key.
1. Split a tmux pane left-right : `ctrl+b` then `%`
1. Split a tmux pane up-down : `ctrl+b` then double quotes: `"`
1. Zoom in or out of the pane: `ctrl+b` then `z`

# Default Services
In one tmux session you might set up your window with 4 "panes" to start or monitor different 0L services:
- `ol start`: this service orchestrates a number of OL services
- `tail -f ~/.0L/logs/node.log`: this will watch the logs for the `diem-node` service, which is the validator node software.
- `tail -f ~/.0L/logs/tower.log`: this will watch the logs for the ol `tower` service, which does the chained proof-of-delay.
- `tail -f ~/.0L/logs/monitor.log`: this will watch the logs for the ol `ol serve -c` service, which serves this node's web monitor on port 3030.
