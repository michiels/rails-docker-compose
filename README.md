# Rails development with Docker

This repository shows you how to easily share a Rails application development
environment amongst your co-workers, without them having to manually install,
compile, or maintain any dependencies on their local workstations.

The repository setup contains sample files for using Docker and Docker Compose
in a certain way to set up a local dev environment in minutes. The only thing
that your and your co-workers will need to install is Docker and Docker Compose.

The stack in this repository:

* Ruby on Rails 5.1.4
* PostgreSQL database
* Redis database
* Sidekiq for background jobs
* Standard Rails asset compilation with Yarn support

Changed files compared to regular Rails app:

* database.yml
* Dockerfile
* docker-compose.yml

## Getting Started

1. Copy `docker-compose.yml` into your own application.

2. Copy `Dockerfile` into your own application.

3. Edit `docker-compose.yml` and change **railsdockercompose_web** to
   **yourapplication_web** for the `image:` keys under `web:` and `sidekiq:`.

Now your own application is set up and you can follow the regular development
environment instructions:

## Start your development environment

*You could copy-paste the following steps  into your own Rails app's README, so
that anyone contributing knows how to get a development environment up and
running.*

To set up your local development environment, we'll be using a piece of software
called Docker. We then use Docker Compose configuration that's
present in this repository to get all required software for running this
application on your own workstation.

First, install Docker for your workstation: https://www.docker.com/community-edition

Then open a terminal and use the  `docker-compose` commands to set up a local
environment:

```
$ cd ~/path/to/my/application
$ docker-compose run --rm web /bin/bash
# rails db:setup
```

Open up another tab in your terminal, or exit the shell session inside the
container again via Control-D.

Then, start the local development server:

```
$ docker-compose up
```

To stop your local development environment again where you're finished working:

```
$ docker-compose stop
```

### Migrating, running tests, etc.

To do any regular Rails task like creating migrations, running tests, or
generating models and controllers, you can use the following command to
keep a development shell open inside the Rails environment:

```
$ docker-compose run --rm web /bin/bash
```

Recommended is to just keep this command open in a terminal so that you
can always access development tasks in Rails.

### Running tests

You can run tests via:

```
$ docker-compose run --rm web /bin/bash
# rails test
```

### Running DB migrations

You can run database migrations via:

```
$ docker-compose run --rm web /bin/bash
# rails generate migration AddAColumnToATable column:string
# rails db:migrate
```

### Modifying Gemfile

After you've made a change to the Gemfile, you need to rebuild your local Docker
container image via docker-compose and restart the local development server:

```
$ docker-compose down
$ docker-compose build
$ docker-compose up
```

## License

This repository is licensed MIT.

## Author

Michiel Sikkes <michiel@firmhouse.com>
