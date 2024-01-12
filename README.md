# CLI Template
This file has instructions on how to setup kubernetes and create pods.
You can execute the commands as instructed.
## Requirments
To get started get these things ready
* Linux server
* SSH connection to your server

That's it, and you can get started
## Setup kubernetes
Get a google cloud key
```console
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key --keyring /usr/share/keyrings/cloud.google.gpg add -
```
Add kubernetes repo
```console
    echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
```
Update `apt` just in case
```console
apt update
```
Download kubernetes (if you get any errors make sure you did everything right before this command)
```console
apt install -y kubelet=1.20.0-00 kubeadm=1.20.0-00 kubectl=1.20.0-00
```
Set commands as hold (Just do it to avoid future problems)
```console
apt-mark hold kubelet kubeadm kubectl
```
```console
```
```console
```
```console
```
```console
```

The above generated a starter CLI project called `mycli` with a working hello command.  The created project also has starter specs for you 😁

    $ rake
    Mycli::CLI
      mycli
        should hello world
        should goodbye world

    Finished in 1.12 seconds (files took 0.71706 seconds to load)
    2 examples, 0 failures

### Subcommands

Use the `--subcommand` to have the generator also include a subcommand example.

    cli-template new mycli --subcommand
    cd mycli
    exe/foo sub goodbye # subcommand example

## Release

Once you are satisfied with the CLI tool, you can release it as a gem.

    1. edit the mycli.gemspec
    2. edit lib/mycli/version.rb
    3. update the CHANGELOG.md

And run:

    rake release

When installed as a gem, you no longer have to prepend exe in front of the command.  For example, `exe/mycli` becomes the `mycli` command.

## Different starter templates

There are 2 different templates that the tool generates from:

1. basic thor project: A standard CLI tool based on basic usage of Thor.
2. colon namespaced project: The generated CLI project still uses Thor but it does some manipulation in order to allow defining namespaced methods with colons instead of spaces.  Example: `mycli sub:command` vs `mycli sub command`.

To use the different templates:

    TEMPLATE=colon_namespaces cli-template new mycli
    TEMPLATE=default cli-template new mycli
    cli-template new mycli # same as TEMPLATE=default

## Auto Completion

There is support for TAB completion in the newly generated CLI project for the default template.  To enable auto completion, add this to `~/.bashrc` or `~/.profile`:

    eval $(mycli completion_script)

Remember to re-load the shell. Note, the auto completion will only work if the cli command is avaialble in your PATH.  You can do this by installing the gem.  You can also create a wrapper bash script that calls to your development cli command like so:

    cat > /usr/local/bin/mycli << 'EOL'
    #!/bin/bash
    exec ~/src/mycli/exe/mycli "$@"
    EOL
    chmod a+x /usr/local/bin/mycli

### Experimental Auto Completion Support for colon_namespaces Template

The auto-completion for the colon_namespaces template CLI project is experimental. Ran into a few issues:

1. Slow as to make auto-completion useless. This because the generated CLI invokes autoloading when it detects the methods for the completion words. Ideas on speeding this would be appreciated! Right now it takes about 1 second.
2. Does not work with colons currently.  Will have to look into this post [Bash Command-Line Tab Completion Colon Character
](https://stackoverflow.com/questions/25362968/bash-command-line-tab-completion-colon-character).
3. Does not work with the last two characters are `--`.

Suggestions to are appreciated!

## Installation

    gem install cli-template

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am "Add some feature"`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
