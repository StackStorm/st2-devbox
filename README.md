# StackStorm Development Container

Somewhat of a drop-in replacement for https://github.com/StackStorm/st2devenv that you don't have to build every time you need it.

## Usage

If you just want to get to st2 development, this command is for you:

```
docker run -it --rm -p 80:80 -p 443:443 -v $(pwd)/../st2:/st2 -v $(pwd)/../st2web:/st2web --name devbox stackstorm/devbox
```

It will run a container with everything StackStorm needs already set up and configured. All you have to do is to provide it with externally mounted codebase of st2 (and st2web, if you want). The container will automatically run `launchdev.sh start` in the `/st2` folder and `gulp serve` in `/st2web` folder. The process of compiling `st2web` should be performed externally via `gulp watch` for better performance. The container will also expose http and https ports for consumption.

Don't forget that you can always execute a command over running container via:

```
docker exec -it devbox <command>
```

For example, you can restart st2 using this line:

```
docker exec -it devbox /st2/tools/launchdev.sh restart
```

## Improving the container

If, on the other hand, you think you can improve the container, feel free to clone the repo, make the changes you see fit and then call:

```
docker build -t stackstorm/devbox .
```

And don't forget to push it back when you're done, we'd like to see how the dev process could be improved.