# Federation Development

## Setup

If you don't have a local clone of the Lemmy repo yet, just run the following command:

```bash
git clone https://github.com/LemmyNet/lemmy
```

## Running locally

You need to have the following packages installed, the Docker service needs to be running.

- docker
- docker-compose
- cargo
- yarn

Then run the following
```bash
cd docker/federation
./run-federation-test.bash -yarn
```

The federation test sets up 3 instances:

Instance / Username | Location
--- | ---
lemmy_alpha | [127.0.0.1:8540](http://127.0.0.1:8540)
lemmy_beta | [127.0.0.1:8550](http://127.0.0.1:8550)
lemmy_gamma | [127.0.0.1:8560](http://127.0.0.1:8560)

You can log into each using the instance name, and `lemmy` as the password, IE (`lemmy_alpha`, `lemmy`). 

Firefox containers are a good way to test them interacting.

## Integration tests

To run a suite of suite of federation integration tests:

```bash
cd docker/federation-test
./run-tests.sh
```

## Running on a server

Note that federation is currently in alpha. **Only use it for testing**, not on any production server, and be aware that turning on federation may break your instance.

Follow the normal installation instructions, either with [Ansible](administration_install_ansible.md) or
[manually](administration_install_docker.md). Then replace the line `image: dessalines/lemmy:v0.x.x` in 
`/lemmy/docker-compose.yml` with `image: dessalines/lemmy:federation`. Also add the following in
`/lemmy/lemmy.hjson`:

```
    federation: {
        enabled: true
        tls_enabled: true,
        allowed_instances: example.com,
    }
```

Afterwards, and whenever you want to update to the latest version, run these commands on the server:

```
cd /lemmy/
sudo docker-compose pull
sudo docker-compose up -d
```
