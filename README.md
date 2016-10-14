## Quick Start

    curl -L https://github.com/rentzsch/ansible-minimal-ec2-xenial/archive/master.tar.gz | tar -xz

    # Replace FILLMEIN with your host
    # for example: ec2-52-33-114-69.us-west-2.compute.amazonaws.com
    $EDITOR ansible-minimal-ec2-xenial-master/inventory

    ./run.sh

## Backgrounder

A minimal ansible template that:

1. Showcases a tiny-but-working ansible setup.

    You could walk up to ansible cold, look at these files and puzzle things out pretty quickly.

2. Works-around OS X / macOS having an allergy to using long domain names.

    I like to use AWS EC2's long domain names (`ec2-52-33-114-69.us-west-2.compute.amazonaws.com`) instead of the plain IP addresses (`52.33.114.69`) since they stick out as obvious EC2 machines. Makes it easier to delete them as they accumulate in my `~/.ssh/known_hosts`.

    Problem is using long domain names runs into an obscure limitation that file socket path length max out at 108 characters. That limitation and its work-around is [documented here](http://docs.ansible.com/ansible/intro_configuration.html#control-path).

    While the project is has EC2 in its name, it actually has nothing directly to do with EC2 other than domain name length. It should be usable with any Xenial machine you can ssh into.

3. Works-around Ubuntu Server 16.04 LTS Xenial lacking Python 2.

    Python is no longer included by default in Ubuntu Server, so Ansible's initial fact-gathering fails (as it requires Python on the target).

    This playbook disables fact-gathering for a quick raw ssh command that quickly tests whether python is installed at all and if not installs `python-minimal`. That sets the stage so the next set of tasks can correctly gather facts and operate normally.

    [Source](https://gist.github.com/gwillem/4ba393dceb55e5ae276a87300f6b8e6f).