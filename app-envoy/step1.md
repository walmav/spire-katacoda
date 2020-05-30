# Deploy SPIRE server and agent

When this page is displayed, a script starts to deploy SPIRE into the
environment, using a join token to attest the agent. See the *SPIRE
using join tokens in docker* scenario to learn more about this and
manually go through what this scenario does automatically.

**Please wait until you see a SPIRE registration entry (`Entry ID :
...`) and a shell prompt (`host01 $`) before continuing.**

# Logs

As you go through this demo, you may want to check the SPIRE Server
and Agent logs to see how various actions affect each of them.

To view the `spire-server` log:

`cat spire-server.log`{{execute}}

To view the `spire-agent` log:

`cat spire-agent.log`{{execute}}
