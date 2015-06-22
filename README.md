Summary
-------

SSH server image with emacs editor. This image allow to download/upload files from/to volumes of a data only containers. It allow to browse the volumes and edit files.


Build the image
---------------

To create this image, execute the following command in the docker-sshd folder.

    docker build -t cburki/sshd .


Configure the image
-------------------

You can configure the SSH root password and authorized key with the following environment variables.

 - SSH_PASSWORD : The root password.
 - SSH_AUTHORIZED_KEY : A key that will be added to the authorized key file of the root user.


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
