# Supported tags and respective `Dockerfile` links

- latest [(Dockerfile)](https://github.com/dfilion/centos6-jenkins-docker/blob/master/Dockerfile)

For more information about this image please see the [GitHub repo](https://github.com/dfilion/centos6-jenkins-docker).

# What is centos6-jenkins?

centos6-jenkins is an image that provides a 64-bit CenOS6 ssh Jenkins client.

# Why centos6-jenkins?

I created this image to use with the Jenkins-CI Docker plugin.  While the 
Docker plugins author provides a Debian based image, I required a CentOS 6 based image.

# Usage

## Basic Usage
While this image is meant to be used by Jenkins-CI, you can run it just like any
other image.

```
docker run -d -P rainingpackets/centos6-jenkins
```

## User password
The running image is accessed using SSH using the credentials:

Username: jenkins
Password: jenkins

## Advanced Usage

### Providing a authorized keys file for the Jenkins user
An alternative to using the username/password combination is to provide an 
authorized_keys file when starting the image.

Specify the authorized_keys file by start the image and passing the file name
in the JENKINS_AUTHORIZED_KEYS environment variable and mounting the directory
containing the file to the /key volume.
```
docker run -d -P -v /jenkins/keys:/keys -e JENKINS_AUTHORIZED_KEYS="jenkins.rsa_id.pub" centos6-jenkins-docker:latest
```
On startup the image will copy the `jenkins.rsa_id.pub` file from the `/keys` directory to the the Jenkins .ssh directory
and rename it `authorized_keys`.

### Disabling the password
If you are using SSH keys, you may decide to disable the jenkins user password.
To disable password based logins, set the environment variable JENKINS_DISABLE_PASSWD
to any value. This causes the entry point script to disable password based
logins in the sshd configuration file.


# SSH Host keys
New SSH host keys are generated on every execution of the image.
Static SSH host keys are not yet supported


# Usage Examples

## Basic usage

* Launch the image
```
docker run -d -p 2222:22 centos6-jenkins-docker:latest
```
* Connect using ssh
```
ssh -p 2222 jenkins@localhost
```

### Provide an authorized SSH key
* Launch the image
```
docker run -d -p 2222:22 -v /home/centos/keys:/keys -e JENKINS_AUTHORIZED_KEYS="jenkins.rsa_id.pub" centos6-jenkins-docker:latest
```
* Connect using the private key
```
ssh -i /home/centos/keys/jenkins.rsa_id -p 2222 jenkins@localhost
```
* Connect using the password
```
ssh -p 2222 jenkins@localhost
```

### Provide and authorized key and disable password based logins.
```
docker run -d -p 2222:22 -v /home/centos/keys:/keys -e JENKINS_AUTHORIZED_KEYS="jenkins.rsa_id.pub" -e JENKINS_DISABLE_PASSWD=1 centos6-jenkins-docker:latest
```
* Connect using the private key
```
ssh -i /home/centos/keys/jenkins.rsa_id -p 2222 jenkins@localhost
```
* Connect using the password
```
ssh -p 2222 jenkins@localhost
```



# Building the image
```
docker build -t centos6-jenkins-docker:latest .
```






