# booklore-snap

[![Get it from the Snap Store](https://snapcraft.io/en/dark/install.svg)](https://snapcraft.io/booklore)

BookLore is a self-hosted web app for organising and managing your personal book
collection. It provides an intuitive interface to browse, read, and track your
progress across PDFs and eBooks. With robust metadata management, multi-user
support, and a sleek, modern UI, BookLore makes it easy to build and explore
your personal library.

**This is an unofficial snap.** After installing, and waiting for the the various
services to start, your instance will be accessible at http://localhost:41935

You'll probably want to connect the snap as follows to allow access your books
which should be in `/mnt/somewhere` or `/media/somewhere` so that the snap can access them:

```bash
sudo snap connect booklore:removable-media
sudo snap connect booklore:mount-observe
```

There are three services, nginx (the web server), booklore-api (the backend API server),
and mariadb (the database server). The database files and logs are stored in the snap's
data directory, which is preserved across snap updates.

You can change the port that each service uses with the following commands:

For the port that nginx listens on (default 41935):

```bash
sudo snap set booklore port=<desired-port>
```

For the port that MariaDB listens on (default 41936):

```bash
sudo snap set booklore database-port=<desired-port>
```

For the port that booklore-api listens on (default 41937):

```bash
sudo snap set booklore api-port=<desired-port>
```

After changing the ports, you will need to restart the snap for the changes to take effect:

```bash
sudo snap restart booklore
```

If you need to connect to the MariaDB database from outside the snap, the username is `booklore`
and you can use the following command to get the password:

```bash
snap get booklore database-password
```

You can also connect with the following command as root:

```bash
sudo mariadb --socket=/var/snap/booklore/common/run/mysql/mysqld.sock -u root --skip-ssl
```
