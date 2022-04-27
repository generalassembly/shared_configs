# Shared Semaphore Config

## [.semaphore/](https://github.com/generalassembly/shared_configs/tree/master/semaphore/.semaphore)

This directory contains shared config that can be automatically copied over to other repos.

The directory structure matches the standard `.semaphore` directory in each repo.

## [templates/](https://github.com/generalassembly/shared_configs/tree/master/semaphore/templates)

This directory contains templates that can be manually copied over to other repos and committed.

Some of these files need to exist at the time of Semaphore's `checkout` which is why they can't be automatically copied
over later.

## Setup

Each repo needs a `setup-shared-config` Semaphore script:

``` bash
touch .semaphore/bin/setup-shared-config
chmod +x .semaphore/bin/*
```

Contents of [.semaphore/bin/setup-shared-config](https://github.com/generalassembly/shared_configs/tree/master/semaphore/templates/bin/setup-shared-config):

``` bash
#!/usr/bin/env -S bash -e

# https://github.com/generalassembly/shared_configs/tree/master/semaphore

SHARED_CONFIG_REPO=https://github.com/generalassembly/shared_configs
REMOTE_SHARED_CONFIG_DIR=$SHARED_CONFIG_REPO/trunk/semaphore/.semaphore
LOCAL_SHARED_CONFIG_DIR=.semaphore-shared

svn export $REMOTE_SHARED_CONFIG_DIR $LOCAL_SHARED_CONFIG_DIR

cp --recursive --no-clobber $LOCAL_SHARED_CONFIG_DIR/* .semaphore/

```

Call `setup-shared-config` inside the repo's `.semaphore/bin/setup-repo` script:

``` bash
#!/usr/bin/env -S bash -e

export PROJECT_DIR=$PWD
export SEMAPHORE_DIR=$PROJECT_DIR/.semaphore
export SEMAPHORE_BIN_DIR=$SEMAPHORE_DIR/bin

$SEMAPHORE_BIN_DIR/setup-shared-config # insert this line after the SEMAPHORE_BIN_DIR export above

export PATH=./bin:$PATH:$SEMAPHORE_BIN_DIR
```

The script will copy the contents of [.semaphore](https://github.com/generalassembly/shared_configs/tree/master/semaphore/.semaphore)
into the repo's `.semaphore` directory without overwriting any existing files.
