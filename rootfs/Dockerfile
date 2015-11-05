FROM heroku/cedar:14

RUN mkdir /app
RUN addgroup --quiet --gid 2000 slug && \
    useradd slug --uid=2000 --gid=2000 --home-dir /app --no-create-home \
        --shell /bin/bash
RUN chown slug:slug /app
WORKDIR /app

# add default port to expose (can be overridden)
ENV PORT 5000
EXPOSE 5000

ADD ./runner /runner
ADD ./bin /bin
RUN chown slug:slug /runner/init
RUN chown slug:slug /bin/mc
USER slug
ENV HOME /app
ENTRYPOINT ["/runner/init"]

ENV DEIS_RELEASE 1.11.0-dev

ONBUILD RUN mkdir -p /app
ONBUILD WORKDIR /app
ONBUILD ADD slug.tgz /app