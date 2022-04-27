# Shared Semaphore Config

## [.semaphore/](.semaphore/)

This directory contains shared config that can be automatically copied over to other repos.

The directory structure matches the standard `.semaphore` directory in each repo.

## [templates/](templates/)

This directory contains templates that can be manually copied over to other repos and committed.

The directory structure matches the standard `.semaphore` directory in each repo.

Some of these files need to exist at the time of Semaphore's `checkout` which is why they can't be automatically copied over later.

## Setup

Each repo needs a [.semaphore/bin/setup-shared-config](templates/bin/setup-shared-config) Semaphore script:

``` bash
touch .semaphore/bin/setup-shared-config
chmod +x .semaphore/bin/*
```

Call `setup-shared-config` inside the repo's `.semaphore/bin/setup-repo` script by inserting it after the `SEMAPHORE_BIN_DIR` export:

``` bash
#!/usr/bin/env -S bash -e

export PROJECT_DIR=$PWD
export SEMAPHORE_DIR=$PROJECT_DIR/.semaphore
export SEMAPHORE_BIN_DIR=$SEMAPHORE_DIR/bin

$SEMAPHORE_BIN_DIR/setup-shared-config

export PATH=./bin:$PATH:$SEMAPHORE_BIN_DIR
```

The script will copy the contents of [.semaphore](.semaphore) into the repo's `.semaphore` directory without overwriting any existing files.
