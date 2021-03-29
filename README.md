# Shared Configs

## Overview

A collection of shared configuration files.

## Contents

* [Scripts](#scripts)
* [Rubocop](#rubocop)

### Scripts

You can call either these scripts directly or add this repository's `scripts`
directory to your `PATH` to easily access them from anywhere.

* [cop-diffs](/dev_tools/scripts/cop-diffs): runs Rubocop on the changed files in your branch
* [scw](/dev_tools/scripts/scw): opens the current Semaphore workflow for your branch

### Rubocop

If this repository is located in `~/code/shared_configs` and you're in the
top-level directory of another project:

**Set up symlink:** `ln -s ~/code/shared_configs/dev_tools/rubocop/ .rubocop`

#### Rubocop resources:

* [Sublime](https://www.sublimetext.com/) package:
  [SublimeLinter-rubocop](https://github.com/SublimeLinter/SublimeLinter-rubocop)
