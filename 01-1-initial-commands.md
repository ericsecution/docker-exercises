# Docker Basics - Initial Commands
<br />

*additional notes and commentary made by me, Eric Mangin, to provide extra details on things that may be of interest or helpful to anyone else as we learn how to navigate Docker together* 🙂👍

## Exercise 01-1.1: Docker Images
note:
- Docker **images** are immutable and so also referred to as snapshots. An **image** contains the definitions of all the libraries, binaries, configuration files, etc. that one would require to run the application. Images are read-only.
- **Containers**, on the other hand (which we'll get into more later on), are instances of these images.

🤔
- For me (even though it's not the same thing), I'm reminded of when I learned about a **Class** vs an **Object** in Java: where the object is an instance of the class, which is more like a "blueprint" of the object.

🧐

Alright, well, before we get too confused by going back and forth from a birdseye view, let's zoom-in and get into some specifics.

Command:
```bash
docker images
```

Output:
```lua
└─[$]> docker images
REPOSITORY                     TAG       IMAGE ID       CREATED         SIZE
docker1/docker101tutorial      latest    1a18f0adf26a   2 days ago      28.9MB
docker101tutorial              latest    1a18f0adf26a   2 days ago      28.9MB
alpine/git                     latest    22d84a66cda4   1 week ago      43.6MB
postgres                       13        a4d5977013bf   2 weeks ago     373MB
archmd/cd                      2.0.6     d78af3215b86   2 weeks ago     169MB
```

note: 
- you might not see any images here yet, it's all good. They'll start to populate (and you can always re-run this command to view them) once we start pulling some in. 
- Your Output will either look like the Header here, but with no images listed underneath, or, the Header with the images, etc listed underneath, in your Terminal.  
<br />

addt'l note: 
- I'm just using an integrated terminal window within VSCode, so I can copy/paste into my Markdown file here more easily, but you can use any Terminal instance that you want. 
- If my Terminal results look different, it's because I'm using some particular theme (I don't even recall which, tbh) within 'zsh' because it's cool, but you can use the default, or 'bash' or whatever you'd like.

<br />

**Docker Docs 🔗**
- **[docker images](https://docs.docker.com/engine/reference/commandline/images/)** are a key component of Docker. 

- They are *read-only* templates that you use to create Docker containers. 

- I've seen these referenced as the "blueprints" for Docker containers.

- With `docker images` you can view the Docker images that are currently available on your system. 

<br />

## Exercise 01-1.2: Image Grab - docker pull

I already have the 'alpine' image (i.e. a minimal Docker image from Alpine Linux), that I've practiced on before, and seems like a fairly common image for many people to start out with, but just going to pull again for good measure. Feel free to compare Outputs.

note: 
- inside of the Docker Desktop app you can also click the 'play' button icon to 'Run', or click the 3-dots menu for 'more actions' ('View Details', 'Pull', 'Push to Hub')
- within the app, I also clicked 'Update to latest' at the top, and then 'Apply and Restart' at the bottom, once it lights up and allows you to click it.

Command:
```bash
docker pull alpine
```

Output:
```lua
└─[$]> docker pull alpine
Using default tag: latest
latest: Pulling from library/alpine
31e352740f53: Pull complete 
Digest: sha256:82d1e9d7ed48a7523bdebc18cf6290bdb97b82302a8a9c27d4fe885949ea94d1
Status: Downloaded newer image for alpine:latest
docker.io/library/alpine:latest
```

(random) Notes:
**What Does that 'sha256:82d1...' Thing Mean?**
- it's a way for Docker (or any container tech) to uniquely identify images and ensure data integrity: same hash = same (unaltered) image
- it's used in various security applications and protocols, including TLS and SSL, PGP, SSH, IPsec, and Bitcoin, among others
- The `sha256:` here denotes a cryptographic hash. The Secure Hash Algorithm (SHA) 256 generates a unique, 256-bit (*32-byte*) hash value for the Docker image.

**Bitcoin, You Say?**
- Mhm, SHA-256 is used in the creation of bitcoin addresses to improve security and privacy. 
- Most notably: the Bitcoin protocol uses a double SHA-256 hash to compute the hash of the block header to produce the actual 'proof-of-work'
- also used within the protocol in other ways
- More about SHA-256 as it relates Bitcoin can be found at this [Bitcoin Wiki](https://en.bitcoin.it/wiki/Hash_function).

<br />

**Docker Docs 🔗**
- **[docker pull](https://docs.docker.com/engine/reference/commandline/pull/)** is used to fetch an image from a Docker registry. 

- `docker pull` stores it locally on your machine.

- This is how you obtain images that you don't already have.

- Or, update those you *do* have to their latest versions. 

<br />

## Exercise 01-01.3: Running A Docker Container

note: 
- I kept having a weird issue the first few times I tried to run the following command (my terminal would just produce a ' >' and require that I 'ctrl-c' to exit out of it). 
- I uninstalled and reinstalled Docker, and was about to switch my terminal (back to 'bash' from 'zsh' on my MacBook, or switch over to a PC), but then noticed that, for whatever reason, the command that I kept navigating back to was missing the closing double-quote ("), and I added that in, and bam, actual expected output. 
- So don't sweat it if you run into some snags--esp for this early stuff. 
- Probably a simple fix, and sometimes just takes a fresh set of eyes or a few mins break to see it from another POV.🫸 👀 💪😎👍

<br />

Command:
```bash
docker run alpine echo "Hello from Docker"
```

Output:
```lua
└─[$]> docker run alpine echo "Hello from Docker"
Hello from Docker
```

<br />


**Docker Docs 🔗**
- The **[docker run](https://docs.docker.com/engine/reference/commandline/run/)** command starts a new container from a given image.

- The container runs a command specified at the end of the docker run command line.

- `docker run` is a core command in Docker, essentially providing the functionality of starting your application in an isolated environment. 

<br />

---

<br />

# Managing The Lifecycle

## Exercise 01-1.4: Listing Docker Containers

- this command: `docker ps` is used to list all running Docker containers
- use `docker ps -a` to see all containers (not just the running ones)

<br />

Command: 
```bash
docker ps
```

Output:
```lua
└─[$]> docker ps                                 
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```
Command:
```bash
docker ps -a
```

Output:
```lua
└─[$]> docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED              STATUS                      PORTS     NAMES
7c959a0534ef   alpine    "echo 'Hello from Do…"   About a minute ago   Exited (0) 36 seconds ago             flamboyant_lichterman
c399022e7140   alpine    "echo 'Hello from Do…"   5 minutes ago  ago   Exited (0) 5 minutes ago              condescending_agnesi
c099fc3de34c   alpine    "/bin/echo 'Hello fr…"   10 minutes ago       Exited (0) 10 minutes ago             vibrant_chatterjee
11613d857e2a   alpine    "/bin/echo 'Hello fr…"   1 hour ago           Exited (0) 1 hour ago                 happy_mcnulty
```
<br />

note:
- When a Docker container is created you can use the `--name <container_name>` flag
- however, if none is provided [Docker provides a name for you](https://agarwalrounak.medium.com/default-container-names-in-docker-15bdbf56b539) *(link to Rounak Agarwal's Medium article)* 
- using this particular [names-generator_test.go](https://github.com/docker/docker-ce/blob/master/components/engine/pkg/namesgenerator/names-generator.go) written in Go *(link to GitHub Repo)*.

**Docker Docs 🔗**

- When using **[docker ps](https://docs.docker.com/engine/reference/commandline/ps/)**, you can add a `--filter` tag and a `--format` option to gain even greater control over the results.

<br />

Here's an example (from the Docker Docs) of both `--format` and `--filter`:

- first identifying the id of the network 'net1':

```lua
docker network inspect --format "{{.ID}}" net1

8c0b4110ae930dbe26b258de9bc34a03f98056ed6f27f991d32919bfe401d7c5
```

- and then taking that id, and using it as a filter:
```lua
docker ps --filter network=8c0b4110ae930dbe26b258de9bc34a03f98056ed6f27f991d32919bfe401d7c5

CONTAINER ID        IMAGE       COMMAND       CREATED             STATUS              PORTS               NAMES
9d4893ed80fe        ubuntu      "top"         10 minutes ago      Up 10 minutes                           test1
```
<br />

---
## Exercise 01-1.5: Stopping Docker Containers

- `docker stop` is used to stop a running Docker container
- you can specify the container that you want to stop by using its ID.

<br />

Command: 
```bash
docker stop <container_id>
```

Output:
```bash
└─[$]> docker stop 7c959a0534ef
7c959a0534ef
```
<br />

note:

- Not a lot of action yet, because we haven't really started running any substantial images just yet.

- A good command to put into your toolbag, nevertheless.

- You don't want to be like me, leaving my snowboarding group lesson (for beginners) shortly after it started, thinking, "Easy. I got this!" ... and then realizing out there on the "black diamond" (▪️🔷) trail that (oops) I didn't know how to stop 💥🏂

- So yeah, never a bad idea to learn how to **stop** at the beginning.

<br />

**Docker Docs 🔗**
- You can read more about `docker stop`, as well as sending a `--signal`... 
- or waiting a number of seconds by using the `--time` flag...
- when you want to **stop** your container(s) from running **[here in the Docker Docs](https://docs.docker.com/engine/reference/commandline/stop/)**.

---
## Exercise 01-1.6: Removing Docker Containers

- `docker rm` is used to remove Docker containers. You can only remove a Docker container if it's not running, so you may need to stop it first using `docker stop`

- you can specify the container that you want to stop by using its ID.

<br />

Command: 
```bash
docker rm <container_id>
```

Output:
```bash
└─[$]> docker rm 7c959a0534ef
7c959a0534ef
```
<br />

### Using These Commands in Practice

We can also run an Alpine container that will just sit idle.

Command:

```bash
docker run -d alpine tail -f /dev/null
```

This command will run a new container in detached mode (`-d`) from the `alpine` image, and will execute the command tail `-f /dev/null` which does nothing but keep the container running.

Ouput:

```lua
└─[$]> docker run -d alpine tail -f /dev/null
3ace535e152648b5042e2d6f0da6be7f6a7dbe028d44121e97df5c17d96b5fab
```
<br />

- Now, if you run **`docker ps`**, you should see the newly created container in the list of running containers.

    Output:

```lua
    └─[$]> docker ps
CONTAINER ID   IMAGE     COMMAND               CREATED          STATUS          PORTS     NAMES
3ace535e1526   alpine    "tail -f /dev/null"   53 seconds ago   Up 52 seconds             naughty_feynman
```

<br />

- If you want to stop the container, you can do so by running **`docker stop`** followed by the *container ID*.

    *(took a few seconds)* Ouput:

```lua
└─[$]> docker stop 3ace535e1526
3ace535e1526
```

- Finally, you can remove the stopped container by using **`docker rm`** followed by the *container ID*.

    Output:

```lua
└─[$]> docker rm 3ace535e1526                   
3ace535e1526
```

So, now (again), running **`docker ps`** ...

Output:

```lua
└─[$]> docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

<br />

*end of Docker Basics - Initial Commands*

---