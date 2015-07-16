Summary
-------

SSH server image with emacs editor. This image allow to download/upload files from/to volumes of a data volume containers. It allow to browse the mounted volumes and edit the files inside theses volumes.


Build the image
---------------

To create this image, execute the following command in the docker-sshd folder.

    docker build -t cburki/sshd .


Configure the image
-------------------

You can configure the SSH root password and authorized key with the following environment variables.

 - SSH_PASSWORD : The root password.
 - SSH_AUTHORIZED_KEY : Your public key that will be added to the authorized key file of the root user.

You will not be able to log into this container if you do not provide at least one of these variables. Be careful to set a strong password for the root access because it has full access to the volumes you specify to mount when running the container.


Run the image
-------------

When you run the image, you will bind the SSH port 22. Add the containers from which to mount the volumes you would like to access.

    docker run \
        --name sshd \
        --volumes-from <container_id> \
        -d \
        -e SSH_PASSWORD=<your_password> \
        -e SSH_AUTHORIZED_KEY="<your_key>" \
        -p 2222:22 \
        cburki/sshd:latest

You can use multiple --volumes-from parameters to bring together multiple data volumes from multiple containers.