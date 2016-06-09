# Drone on docker-compose

This repository contains a minimal example of Drone running within [docker-compose](https://docs.docker.com/compose/overview/). This is a quick and easy way to experiment with Drone.
  
## Dependencies

We recommend:

* [docker-compose](https://docs.docker.com/compose/install/) >= 1.7.0
* [Docker Engine](https://docs.docker.com/engine/installation/) >= 1.10

## How this works

docker-compose reads the `docker-compose.yml` file and spins up two containers:

* Drone Server
* Drone Agent

The former serves the web UI and responds to webhooks. The latter runs the builds. The Drone Server's port 8000 is mapped to the host and bound on 0.0.0.0. You'll need to expose this port to Github for it to be able to receive push/PR/tag webhooks.

## Quickstart

* Add a Drone OAuth application in your [Github settings](https://github.com/settings/profile). This can be done on your account, or on any organization that you have sufficient permissions to. Use something like this as your authorization callback url: `http://drone.mycompany.com:8000/authorize`
* Open `docker-compose.yml`. Search for "`CHANGEME`" and change the values as directed. Make sure to substitute your Github OAuth application credentials.
* run `docker-compose up`
* Make port 8000 on the machine you are running this on open to the internet.
* Point your browser at `http://drone.mycompany.com:8000`. Profit.

## Notes

A few things to keep in mind:

* This setup is designed to be runnable as a non-root user and to avoid conflicting with existing services, hence the port 8000 binding. Feel free to change this to suit your preferences.
* Data is persisted to the `drone-data` directory, which ends up being a sibling to the `docker-compose.yml` file. If you delete this directory and restart the Drone Server, you'll end up starting fresh.

## Tips

* This demo does not include HTTPS, which is generally a good idea for production installs.
* You can adapt this manifest to run on Docker Swarm [reasonably easily](https://docs.docker.com/compose/swarm/), if you desire.
* You can scale the number of agents servicing builds like this: `docker-compose scale drone-agent=3`

## Stuck? Need help?

We've glossed over quite a few details, for the sake of brevity. If you have questions, post them to our [Help!](https://discuss.drone.io/c/help) category on the Drone Discussion site. If you'd like a more realtime option, visit our [Gitter room](https://gitter.im/drone/drone).

## Contributions welcome!

If you have anything to add or improve, please don't hesitate to send
pull requests.

## License

The contents of this repository are licensed under the Apache 2.0 License.
