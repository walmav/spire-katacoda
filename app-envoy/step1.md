# Deploy SPIRE server and agent

This demo uses a script to deploy SPIRE into the environment, using a join
token to attest the agent. See the `SPIRE using join tokens in docker`
scenario to learn more about this and manually go through what this scenario
does automatically.

# Logs

To view the `spire-server` log:

`cat spire-server.log`{{execute}}

To view the `spire-agent` log:

`cat spire-agent.log`{{execute}}

**Please wait until you see a SPIRE registration entry and a shell prompt
before continuing.**
