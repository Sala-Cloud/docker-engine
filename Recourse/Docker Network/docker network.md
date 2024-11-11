# Networking with Standalone Containers

This series of tutorials deals with networking for standalone Docker containers. For networking with swarm services, see **Networking with swarm services**. If you need to learn more about Docker networking in general, see the overview.

This topic includes two different tutorials. You can run each of them on Linux, Windows, or a Mac, but for the last one, you need a second Docker host running elsewhere.

- **Use the default bridge network** demonstrates how to use the default bridge network that Docker sets up for you automatically. This network is not the best choice for production systems.
- **Use user-defined bridge networks** shows how to create and use your own custom bridge networks to connect containers running on the same Docker host. This is recommended for standalone containers running in production.

Although overlay networks are generally used for swarm services, you can also use an overlay network for standalone containers. This is covered as part of the tutorial on using overlay networks.

## Use the Default Bridge Network

In this example, you start two different alpine containers on the same Docker host and do some tests to understand how they communicate with each other. You need to have Docker installed and running.

1. Open a terminal window. List current networks before you do anything else. You may see different networks, but you should at least see these (the network IDs will be different):

   ```bash
   docker network ls
   ```

   Output:

   ```plaintext
   NETWORK ID          NAME                DRIVER              SCOPE
   17e324f45964        bridge              bridge              local
   6ed54d316334        host                host                local
   7092879f2cc8        none                null                local
   ```

   The default bridge network is listed, along with host and none. The latter two are not fully-fledged networks but are used to start a container connected directly to the Docker daemon host's networking stack, or to start a container with no network devices.

2. Start two alpine containers running ash (Alpine's default shell):

   ```bash
   docker run -dit --name alpine1 alpine ash
   docker run -dit --name alpine2 alpine ash
   ```

3. Check that both containers are actually started:

   ```bash
   docker container ls
   ```

   Output:

   ```plaintext
   CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
   602dbf1edc81        alpine              "ash"               4 seconds ago       Up 3 seconds                            alpine2
   da33b7aa74b0        alpine              "ash"               17 seconds ago      Up 16 seconds                           alpine1
   ```

4. Inspect the bridge network to see what containers are connected to it:

   ```bash
   docker network inspect bridge
   ```

   Output:

   ```json
   [
       {
           "Name": "bridge",
           "Id": "17e324f459648a9baaea32b248d3884da102dde19396c25b30ec800068ce6b10",
           "Scope": "local",
           ...
       }
   ]
   ```

   Notice that under the `Containers` key, each connected container is listed with its IP address.

5. Use the `docker attach` command to connect to `alpine1`:

   ```bash
   docker attach alpine1
   ```

   Inside `alpine1`, use `ip addr show` to see network interfaces:

   ```bash
   ip addr show
   ```

6. Verify internet connectivity by pinging an external address:

   ```bash
   ping -c 2 google.com
   ```

7. Now try pinging the second container by IP:

   ```bash
   ping -c 2 172.17.0.3
   ```

   Attempting to ping by container name will fail:

   ```bash
   ping -c 2 alpine2
   ```

8. Detach from `alpine1` with `CTRL + p CTRL + q`.

9. Stop and remove both containers:

   ```bash
   docker container stop alpine1 alpine2
   docker container rm alpine1 alpine2
   ```

**Note:** The default bridge network is not recommended for production.

## Use User-Defined Bridge Networks

1. Create the `alpine-net` network:

   ```bash
   docker network create --driver bridge alpine-net
   ```

2. List Docker's networks:

   ```bash
   docker network ls
   ```

3. Inspect the `alpine-net` network:

   ```bash
   docker network inspect alpine-net
   ```

4. Create four containers and connect them to networks as needed:

   ```bash
   docker run -dit --name alpine1 --network alpine-net alpine ash
   docker run -dit --name alpine2 --network alpine-net alpine ash
   docker run -dit --name alpine3 alpine ash
   docker run -dit --name alpine4 --network alpine-net alpine ash
   docker network connect bridge alpine4
   ```

5. Verify that all containers are running:

   ```bash
   docker container ls
   ```

6. Inspect both networks (`bridge` and `alpine-net`) again:

   ```bash
   docker network inspect bridge
   docker network inspect alpine-net
   ```

7. **Attach to alpine4** and ping other containers to test network connectivity.

## Conclusion

User-defined bridge networks are better suited for production, providing more control over container communication.
