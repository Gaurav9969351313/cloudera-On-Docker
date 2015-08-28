# Docker container for Cloudera Base Nodes

This docker files shows how to build your own base image for various cloudera components running on Centos6.6

## Docker instructions
* Centos 6.6 - will be used as the base
* Install the necessary packages like wget,sudo, ssh etc
* Configure sudo for password key based login & create hadoop admin uid with keys
* Disable IP Tables, Selinux ( by default selinux is disabled in centos6.6 & *Cloudera doesn't like Selinux as of now* )
* Setup the Cloudera yum repo, import GPG Key
	* Install Java
	* Install core hadoop components
	* Clean up the repos,
	* Start SSHD
* Build the image

Known Issues:

> Cloudera does not like hyphen "-" in hostnames, some times it breaks during managed installations.

### Build your image

Build your image using the dockerfile `docker build --tag="local/clouderabasenode:v1" .`

### Run as container
* _I recommend running weave before starting this node, as Weave DNS takes care of the Hostname/IP Constraints required by Cloudera & It likes the container to run in privileged mode_
* Below syntax only opens the cms server port, you might want add more ports as you need.

```
docker run -dti --name clouderabasenode \
				-p 2891:22 \
				--privileged=true \
				mystique:clouderabasenode:latest

```
##### To Do
* Expose the necessary ports ( there is a whole lot of them ).
* Probably can add zookeeper client also.

