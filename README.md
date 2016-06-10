
A simple setup which creates Vagrant boxes installs Docker on each and configures Rancher server on master box.

The other boxes can be used to setup Mesos/Swarm/Kubernetes/Cattle orchestration engines as per your choice.

Following parameters can be tweaked to taste.

MASTER_MEMORY=1024
AGENT_MEMORY=1024

RANCH_SUBNET="172.19.8"
RANCH_MASTER_ADDRESS="172.19.8.100"