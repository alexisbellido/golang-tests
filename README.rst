Create a container for Golang tests.

.. code-block:: bash

  $ docker run -it --rm --mount type=bind,source="$(pwd)"/src,target=/go/src --mount type=bind,source="$(pwd)"/bin,target=/go/bin golang:1.14.2-buster bash

Try with private key.

.. code-block:: bash

  $ docker run -it -w /root -v ~/.ssh/id_rsa:/root/.ssh/id_rsa -v $SSH_AUTH_SOCK:/run/ssh_agent -e SSH_AUTH_SOCK=/run/ssh_agent -v "$PWD":/root -p 3999:3999 --name mygo-1 --hostname mygo-1 golang:1.14.2-buster

Removing after exiting.

.. code-block:: bash

  $ docker run -it --rm -p 3999:3999 --name mygo-1 --hostname mygo-1 golang:1.14.2-buster


Start the container later and get a bash command line.

.. code-block:: bash

  $ docker start mygo-1
  $ docker exec -it mygo-1 /bin/bash

You may not need to container running because you can execute commands from the host. Here's just executing a compiled Go program but nothing will continue running later.

.. code-block:: bash

  $ docker run -it -w /root -v "$PWD":/root -p 3999:3999 --name mygo-2 golang:1.14.2-buster ./hello
  $ docker start mygo-2
  $ docker exec -it mygo-2 /bin/bash

For this Go image you can use docker run with /bin/bash or no command at all and will still allow you to start and exec the container later.

.. code-block:: bash

  $ docker run -it -w /root -v "$PWD":/root -p 3999:3999 --name mygo-2 golang:1.14.2-buster /bin/bash
  $ docker start mygo-2
  $ docker exec -it mygo-2 /bin/bash


Inside the container, start gotour making sure you have the hostname pointing to the container's private IP and on the host pointing to 127.0.0.1.

.. code-block:: bash

  $ root@mygo-1:~# go get golang.org/x/tour/gotour
  $ root@mygo-1:~# gotour -http mygo-1:3999
