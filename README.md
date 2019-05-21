# deno_docker

Docker files for [deno](https://github.com/denoland/deno).

These are published on Dockerhub at [hayd/deno](https://hub.docker.com/r/hayd/deno).

For example:

```Dockerfile
FROM hayd/deno:alpine-0.6.0

EXPOSE 1993

WORKDIR /app
ENV DENO_DIR /cache/

# cache the deps as a layer (this is re-run only when deps.ts is modified)
COPY deps.ts /app
RUN deno fetch deps.ts
ADD . /app
# compile the main app so that it doesn't need to be compiled at each startup
RUN deno fetch main.ts

ENTRYPOINT ["deno", "run", "--allow-net", "main.ts"]
```

and run locally:

```sh
$ docker build -t app . && docker run -it --init -p 1993:1993 app
```

See example directory.
