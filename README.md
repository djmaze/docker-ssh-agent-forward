Forward SSH agent socket into a container

## Installation

Assuming you have a `/usr/local`

```bash
$ git clone git://github.com/djmaze/docker-ssh-agent-forward
$ cd docker-ssh-agent-forward
$ make
$ sudo make install
```

On every boot, do:

```bash
$ pinata-ssh-forward
```

and the you can run `pinata-ssh-mount` to get a Docker CLI fragment
that adds the SSH agent socket and set `SSH_AUTH_SOCK` within the container.

```bash
$ pinata-ssh-mount 
-v /Users/avsm/.pinata-sshd/ssh-1azk9Mmd27/agent.16:/tmp/ssh-agent.sock --env SSH_AUTH_SOCK=/tmp/ssh-agent.sock

$ docker run -it `pinata-ssh-mount` ocaml/opam ssh git@github.com
The authenticity of host 'github.com (192.30.252.128)' can't be established.
RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'github.com,192.30.252.128' (RSA) to the list of known hosts.
PTY allocation request failed on channel 0
Hi avsm! You've successfully authenticated, but GitHub does not provide shell access.
Connection to github.com closed.
```

Alternatively, you can try the example [docker-compose.yml](docker-compose.example.yml):

```bash
$ docker-compose -f docker-compose.example.yml run --rm app
```

## Contributors

* Justin Cormack
* Martin Honermeyer

[License](LICENSE.md) is ISC.
