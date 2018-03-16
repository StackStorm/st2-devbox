# StackStorm Development Container

Somewhat of a drop-in dev environment replacement using docker for StackStorm. If you prefer to use Vagrant, use [st2devenv](https://github.com/StackStorm/st2devenv) instead for core StackStorm development.

We also have [Vagrant environment with st2 pre-installed for pack development](https://github.com/StackStorm/st2vagrant) and a [docker evaluation of StackStorm product](https://github.com/StackStorm/st2-docker).

Use this only when you want to develop StackStorm.

## Requirements

[Docker](https://docs.docker.com/install/)

## Usage

First pull the StackStorm docker devbox image from docker hub:
```
docker pull stackstorm/devbox
```

If you just want to get to st2 development, this command is for you:

```
docker run -it --rm -p 80:80 -p 443:443 -v $(pwd)/../st2:/st2 -v $(pwd)/../st2web:/st2web --name st2devbox stackstorm/devbox
```

It will run a container with everything StackStorm needs already set up and configured. All you have to do is to provide it with externally mounted codebase of st2 (and st2web, if you want). The container will automatically run `launchdev.sh start` in the `/st2` folder and `gulp serve` in `/st2web` folder. The process of compiling `st2web` should be performed externally via `gulp watch` for better performance. The container will also expose http and https ports for consumption.

Don't forget that you can always execute a command over running container via:

```
docker exec -it st2devbox <command>
```

For example, you can restart st2 using this line:

```
docker exec -it st2devbox /st2/tools/launchdev.sh restart
```

To get a shell inside the container:
```
docker exec -it st2devbox /bin/bash
```

## Improving the container

If, on the other hand, you think you can improve the container, feel free to clone the repo, make the changes you see fit and then call:

```
docker build -t stackstorm/devbox .
```

And don't forget to push it back when you're done, we'd like to see how the dev process could be improved.