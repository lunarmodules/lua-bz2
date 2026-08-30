# Releases

## Overview

This document provides guidance to publish a new release for `lua-bz2`.

## Steps before pushing a new tag

1. Create a feature branch for the changes;

2. Bump the version on `LBZ2_VERSION` macro defined in the file `lbz.c`;

> [!IMPORTANT]
> 
> The version assigned to `LBZ2_VERSION` must match the upcoming tag and also the following regex pattern: `^[0-9]+(\.[0-9]+)+$`. Thus, `0.3` is allowed, `0.3.1` is also allowed, but a single number `1` is **NOT** allowed (*unless this pattern is fixed on every spot at [./.github/workflows/publish.yml](./.github/workflows/publish.yml)*).

3. Based on the development rockspec, create a new release rockspec inside the directory `rockspecs` (e.g.: `rockspecs/lua-bz2-0.2.4-1.rockspec`) changing both the rockspec name and the field `local package_version`;

4. Make sure the created rockspec (**CHANGE** `rockspecs/lua-bz2-0.2.4-1.rockspec` below to the new name) prints the expected output running the following script from the terminal or command line:

    ```bash
    lua -e "loadfile(arg[0])(); print(); print('package  :', package); print('version  :', version); print('branch   :', source.branch); print('tag      :', source.tag); print('url      :', source.url); print('homepage :', description.homepage); print();" -- rockspecs/lua-bz2-0.2.4-1.rockspec
    ```

5. Make sure `luarocks make` is able to build the project correctly for the fresh rockspec;

6. Commit the changes and push them to the remote repository;

## Tagging a new release

After all the previous steps were performed:

1. Create a new annotated tag (e.g.: `git tag -a "0.2.4" -m "Release 0.2.4"`) changing `0.2.4` in the previous command to contain the exact **SAME VERSION** on `LBZ2_VERSION` macro defined in the file `lbz.c`;

2. Push the new tag to the remote repository (e.g.: `git push origin 0.2.4`);

## Publish to LuaRocks and GitHub Releases

Once a new tag was released, select the `Publish` action on GitHub Web to trigger it manually:

1. In the UI, select the latest tag pushed in the previous step;
2. Hit the button to run the `Publish` action using the chosen tag.