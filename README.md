# Katacoda demos for SPIRE

## Background

This is a temporary repository, linked to my free Katacoda account. Once we
have our Katacoda contract this repository should be forked into a general
repo in the `scytale` github where it can be linked to the corporate Katacoda
account.

This repo should remain for my own development purposes - and anyone else
working on Katacoda demos would simply clone the general repo (once it exists),
and link that to their own Katacoda account for development. Cloning into a
private, personal repo for development purposes will help insure we don't break
existing Katacoda scenarios that customer's might see.

To put it another way: The general Katacoda repository should be considered
"release" quality, and all development done in private repositories.

## Layout

Things will vary to a fair degree by each individual scenario, and whether they
are using `k8s`, `docker-compose`, or some other deployment method.

In general, scenarios are organized thusly:

+ `assets` contains all the files that need to be copied to the host to run the
  scenario. What happens with files in `assets` is controlled by `index.json` -
  files are explicitly copied to a target directory by filename (or simple
  globbing). Any further moving of files is done in the `configure` script. Note
  Katacoda does **not** allow any subdirectories in `assets`, so this must be
  a flat directory with all files. Some of the scenarios, such as the ones
  based on k8s, use a file naming standard where files are prefixed with the
  name of the eventual target directory and the `configure` script is
  responsible for renaming them where they need to be and the final filename.
  Also note that it can take quite some time for Katacoda to copy up all the
  assets. All scenarios contain some logic that waits for files to be uploaded
  before finishing configuration - be sure to pick a file at the end of the
  `assets` list in `index.json`.
+ `start_env` is a script to bootstrap whatever should be autostarted when the
  scenario is started, such as waiting for k8s to come up, waiting for assets,
  running the `configure` script, and so on. All lines in this script will be
  echoed to the terminal, so it should be as brief and minimal as possible. Put
  everything else in `configure`.
+ `configure` is a script to do additional environment setup, such as rename
  and move files in `assets` as discussed above, waiting for k8s to be actually
  fully up for k8s scenarios (do not rely on `launch.sh` returning - some bits
  of k8s necessary for SPIRE won't be started yet), setting the shell prompt,
  and so on.
+ `waitfor` is a script for `docker-compose` scenarios that waits for a
  container to start.

## Deploying scenarios

Once a scenario repository is correctly linked to a Katacoda account, deployment
involves pushing to the `master` branch of the repository. It'll take a few
minutes for the Katacoda commit hooks to trigger and update.

## Other tips

Debugging Katacoda scenarios when they don't work isn't necessarily easy. If
the environment boots, then it's just a matter of debugging in the environment,
however if (when) the environment doesn't even boot there can be very little
feedback about what Katacoda doesn't like in the scenario.

I found it helpful to run scenarios locally before even trying to run them
in Katacoda. Generally I start with the directory structure the way I want to
see it on the target system and get commands/scripts running locally against
either `k8s` or `docker-compose` as appropriate. Once I can run through the
scenario I move things to assets and decide how they will map into `index.json`
and/or `configure` to get the files where they need to be.
