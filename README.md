# This is a quick demo of how asdf works

See github.com/asdf-vm/adf

## Go to project
```sh
cd project-1
```

## What version of Go do I have?
```sh
go version
```

Whoops, I don't have it installed! Let's install it.

## What plugins do I have?
```sh
asdf plugin-list
```

## Let's add Go to our installed plugins
```sh
asdf plugin-add golang
```

## What versions of Go are available?
```sh
asdf list-all golang
```

## Let's get the latest version
```sh
asdf install golang 1.12.6
```

## Make that the global version
```sh
asdf global golang 1.12.6
```

## Now what version of Go am I running now?
```sh
go version
```

Great, I have the right version.

## Now, let's go to this other Go project
```sh
cd ../project-2
```

## This project requires an older version of Go. Let's install it.
```sh
asdf install golang 1.5.4
```

I can't make that my global version - that'll mess up my other project.

## Let's make it the local version for this project
```sh
asdf local golang 1.5.4
```

## Let's see what version we're using
```sh
go version
```

Great! We're using the right version for this project.

## How is that happening?
```sh
vi .tool-versions
```

## How is the global version set?
```sh
vi ~/.tool-versions
```

asdf traverses up the directory tree and looks for a .tool-versions file to find what version to run

## Well, this tool also needs postgres. What versions do I have installed?
```sh
asdf list postgres
```

## Let's use 9.6.11 for this project - it's an old project
```sh
asdf local postgres 9.6.11
```

## Test the posstgres version
```sh
pg_ctl --version
```

## And see .tool-versions again
```sh
vi .tool-versions
```

## Oh wait, the first project needs postgres, too.
```sh
cd ../project-1
```

But it needs a newer version. When you install PG, it's compiled from source. That takes a few minutes, which is why I'm only demoing with versions I already have installed.

## Let's use 11.3
```sh
asdf local postgres 11.3
```

## We can have multiple versions of postgres installed, but only one version can be running at a time.
```sh
pg_ctl --version
```

# There are a ton of tools you can version with asdf. Check out the asdf list of plugins
```sh
open https://asdf-vm.com/#/plugins-all
```

How does asdf make the right version run?

## When you install a plugin, it creates a file (a shim) in your path that is called when you run the tool.
```sh
which go
```

## That runs asdf's script which finds the .tool-versions file and runs the defined version.
```sh
vi $(which go)
```

## When you want to remove a version
```sh
asdf uninstall golang 1.5.4
asdf list golang
```

## And when you want to remove an entire plugin
```sh
asdf plugin-remove golang
asdf plugin-list
```
