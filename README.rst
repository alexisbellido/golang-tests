Create a container for Golang tests.

.. code-block:: bash

  $ docker run -it -w /root -v ~/.ssh/id_rsa:/root/.ssh/id_rsa -v $SSH_AUTH_SOCK:/run/ssh_agent -e SSH_AUTH_SOCK=/run/ssh_agent -v "$PWD":/root -p 3999:3999 --name mygo-1 --hostname mygo-1 golang:1.8.3-jessie 


Removing after exiting.

.. code-block:: bash

  $ docker run -it --rm -p 3999:3999 --name mygo-1 --hostname mygo-1 golang:1.8.3-jessie 


Start the container later and get a bash command line.

.. code-block:: bash

  $ docker start mygo-1
  $ docker exec -it mygo-1 /bin/bash


Inside the container, start gotour.

.. code-block:: bash

  $ root@mygo-1:~# go get golang.org/x/tour/gotour
  $ root@mygo-1:~# gotour -http 0.0.0.0:3999
