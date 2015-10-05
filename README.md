## What is centos6-jenkins?

centos6-jenkins is an image that provides a CenOS6 ssh Jenkins client.  This image is used as a base for the other Rainingpackets Jenkins images.

## Usage
To run the latest version of the container:

docker run -d -P rainingpackets/centos6-jenkins

## SSH access
You can ssh into the running image using the credentials:

Username: jenkins
Password: jenkins

The ssh host keys are generated on every execution of the image.

Static ssh keys (user or host) are not yet supported.
