# Docker Basics
<br />

*additional notes and commentary made by me, Eric Mangin, to provide extra details on things that may be of interest or helpful to anyone else as we learn how to navigate Docker together* 🙂👍

## Exercise 01-1.1: Docker Images

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

## Exercise 01-1.2: Docker Images

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

