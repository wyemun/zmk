# How to build
1. cd to `app`
2. ```
west build -d build/left -b  nice_nano_v2 -- -DZMK_CONFIG=/workspaces/zmk-config/config -DSHIELD=sofle_left
```

west build -d build/right -b  nice_nano_v2 -- -DZMK_CONFIG=/workspaces/zmk-config/config -DSHIELD=sofle_right

# Problem opening containier in VSCode?
Every now and then, docker container will be problematic, do the following:asa

1. Stop the container by exiting VSCode. You can verify no container is running via the command `docker ps`.
2. Remove all the containers that are not running via the command docker container prune. We need to remove the ZMK container before we can delete the default zmk-config volume referenced by it. If you do not want to delete all the containers that are not running, you can find the id of the ZMK container and use docker rm to delete that one only.
3. Remove the default volume via the command `docker volume rm zmk-config`.
4. Then you can bind the zmk-config volume to the correct path pointing to your local zmk-config folder:
  ```
  docker volume create --driver local -o o=bind -o type=none -o \    device="/wsl/full/path/to/your/zmk-config/" zmk-config
  ```
5. Run vscode "Rebuild and Reopen in Container"