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


# Refreshing all settings

Sometimes you need to update config files located in `~/.0L/`

Usually these files should not be manually edited.

The main config files are:
- `0L.toml` which has default settings for all the 0L tools (tower, transaction sending).
- `key_store.json` contains the private keys for operating then node (note that the "owner" key is not contained there, this is the key that can move GAS coins).
- `validator.node.yaml`: has all the settings for `diem-node` to start as a validator node.
- `fullnode.node.yaml`: has all the settings for `diem-node` to start as a FULLNODE node, which you may have to use when your validator falls out of the validator set.

## Nuclear option: overwrite all files:
Do what would be done at onboarding of the validator, but skip the mining.
```
onboard val --skip-mining --autopay-file <path to your autopay_batch.json file --upstream_peer http://localhost:8080 
```

# Validators with Rotated Keys
Usually any mnemonic derives a default `account address` for those keys. However an account address is decoupled from the mnemonic. Meaning, the account can be linked to a different mnemonic, by "key rotation". Unless you explicitly say so, the 0L tools will assume you are using the *DERIVED ADDRESS* connected to the mnemonic, and you may get failed transactions.

That all said, the solution is to make sure your `0L.toml` file has the intended account address and authkey.

