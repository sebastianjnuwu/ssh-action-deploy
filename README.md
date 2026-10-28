
<p align="center">
  <b>ssh-action-deploy</b>
  <br>
  <smail>"What you were looking for all this time to be here, deploy your application"</smail>
</p>

# About

 Deploy your application to vps over ssh quickly and easily using github actions...<br>
  - Deploy your application 
  - Execute commands
  - Easy and fast 
  - Authenticate with an ssh **key** or with a **password**

# mode of use

 Worth remembering if you have any questions or suggestions just open an [issue](https://github.com/sebastianjnuwu/ssh-action-deploy/issues).
## Warning

 Read this before running <strong>ssh-action-deploy</strong>
 
 • If `FOLDER` is provided, it is cleaned before the copy. Leave it empty to only execute commands (no file deploy).
 
 • `FOLDER` is validated before the cleanup: `/`, `~`, `..`, system directories and paths with special characters are rejected, so a typo cannot wipe the server.

 • `FOLDER` must contain only letters, numbers, `.`, `_`, `/`, `~` and `-` (no spaces).
 
 • `FOLDER` is optional. If omitted, the action only runs `RUN`.
 
 • The ssh port is `22` by default. Set `PORT` to deploy on a different port.

 • If you want to use several commands, separate them with `&` or `;`.

 • You must provide **one** authentication method: `KEY` (private key) or `PASSWORD` — or **both at the same time**: the key authenticates, and the password is there too if you need it.

 • The password mode uses [sshpass](https://sourceforge.net/projects/sshpass/), which is installed automatically on the runner (`apt`, `apk`, `dnf`, `yum` or `brew`).

## example

  It is very simple to use, see the example:
```yml
# Please read the next section below before using for your own safety "variables".
name: 🐥 ssh-action-deploy

on:
  push:
    branches: [ "action" ]
  pull_request:
    branches: [ "action" ]
    
jobs:
  build:
    name: 🕳️ Ubuntu...
    runs-on: ubuntu-latest
    steps:
      - name: 💞 Github actions...
        uses: actions/checkout@v3
      - name: 🌈 Deploy with ssh...
        uses: sebastianjnuwu/ssh-action-deploy@v5
        with:
          IP: ${{ secrets.IP }}
          USER: ${{ secrets.USER }}
          KEY: ${{ secrets.KEY }}
          FOLDER: "/root/.deploy"
          RUN: "ls -a; pwd"
  ```

## example with password

  Only the authentication changes: drop `KEY` and use `PASSWORD`.

```yml
      - name: 🌈 Deploy with ssh password...
        uses: sebastianjnuwu/ssh-action-deploy@v5
        with:
          IP: ${{ secrets.IP }}
          USER: ${{ secrets.USER }}
          PASSWORD: ${{ secrets.PASSWORD }}
          FOLDER: "/root/.deploy"
          RUN: "ls -a; pwd"
  ```

## example with key + password

Provide both `KEY` and `PASSWORD` at the same time — the action accepts the two together.

```yml
      - name: 🌈 Deploy with ssh key and password...
        uses: sebastianjnuwu/ssh-action-deploy@v5
        with:
          IP: ${{ secrets.IP }}
          USER: ${{ secrets.USER }}
          KEY: ${{ secrets.KEY }}
          PASSWORD: ${{ secrets.PASSWORD }}
          FOLDER: "/root/.deploy"
          RUN: "ls -a; pwd"
  ```

  > The password is passed to `sshpass` through the `SSHPASS` environment variable (not on the command line), so it does not show up in the process list.

## example running commands only (no file deploy)

Omit `FOLDER` and use only `RUN`:

```yml
      - name: 🌈 Execute commands...
        uses: sebastianjnuwu/ssh-action-deploy@v5
        with:
          IP: ${{ secrets.IP }}
          USER: ${{ secrets.USER }}
          PASSWORD: ${{ secrets.PASSWORD }}
          RUN: "cd /root/docker && docker compose ps"
```


## example with a custom ssh port

`PORT` is optional and defaults to `22`. Use it when the server listens on another port:

```yml
      - name: 🌈 Execute commands on a custom port...
        uses: sebastianjnuwu/ssh-action-deploy@v5
        with:
          IP: ${{ secrets.IP }}
          USER: ${{ secrets.USER }}
          PORT: "2222"
          PASSWORD: ${{ secrets.PASSWORD }}
          RUN: "uptime"
  ```

## variables 

| variable | example  | require |
| -------- | ----------- | ------- |
| `IP` | `1.1.1.1`| `true` |
| `USER` | `root` | `true` |
| `PORT` | `22` | `false` (default `22`) |
| `KEY` | `xxxxxx` | `false` (required if `PASSWORD` is empty) |
| `PASSWORD` | `xxxxxx` | `false` (required if `KEY` is empty) |
| `FOLDER` | `/root/.deploy`| `false` |
| `RUN` | `uptime` | `false` |
