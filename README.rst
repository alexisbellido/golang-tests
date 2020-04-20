Create a container for Golang tests.

.. code-block:: bash

  $ docker run -it --rm --mount type=bind,source="$(pwd)"/src,target=/go/src --mount type=bind,source="$(pwd)"/bin,target=/go/bin -p 3999:3999 --name mygo-1 --hostname mygo-1 golang:1.14.2-buster bash

Try with a private key in case I need to access private repositories.

.. code-block:: bash

  $ docker run -it -w /root -v ~/.ssh/id_rsa:/root/.ssh/id_rsa -v $SSH_AUTH_SOCK:/run/ssh_agent -e SSH_AUTH_SOCK=/run/ssh_agent -v "$PWD":/root -p 3999:3999 --name mygo-1 --hostname mygo-1 golang:1.14.2-buster

Inside the container, start gotour making sure you have the hostname pointing to the container's private IP and on the host pointing to 127.0.0.1. That's why I'm passing --hostname to docker run (I tried with -http 0.0.0.0:3999 but it didn't work).

.. code-block:: bash

  $ root@mygo-1:~# go get -v golang.org/x/tour
  $ root@mygo-1:~# tour -http mygo-1:3999

Now open http://localhost:3999/.

