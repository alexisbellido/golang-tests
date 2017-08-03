Create a container for Golang tests.

.. code-block:: bash

  $ docker run -it --name mygo-1 golang:1.8.3-jessie


Removing after exiting.

.. code-block:: bash

  $ docker run -it --rm --name mygo-1 golang:1.8.3-jessie



Start the container later and get a bash command line.

.. code-block:: bash

  $ docker start mygo-1
  $ docker exec -it mygo-1 /bin/bash
