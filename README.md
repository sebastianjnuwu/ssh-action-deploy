<p align="center">
  <img src="https://icon-library.com/images/terminal-icon/terminal-icon-1.jpg" width=140 height=140 />
  <br>
  <b>ssh-action-deploy</b>
  <br>
  <smail>"What you were looking for all this time to be here, deploy your application"</smail>
</p>

# About

 Deploy your application to vps over ssh quickly and easily using github actions...<br>
  - Deploy your application 
  - Execute commands
  - Easy and fast 

# mode of use

 Worth remembering if you have any questions or suggestions just open an [issue](https://github.com/sebastianjnuwu/ssh-action-deploy/issues).
## Warning

 Read this before running <strong>ssh-action-deploy</strong>
 
 • During deploy the folder you put in is cleaned.
 
 • We use the default ssh port (22) to execute the deploy

 • If you want to use several commands, separate them with `&` or `;`.

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
        uses: sebastianjnuwu/ssh-action-deploy@v1
        with:
          IP: ${{ secrets.IP }}
          USER: ${{ secrets.USER }}
          KEY: ${{ secrets.KEY }}
          IGNORE: ['README.md','LICENSE']
          FOLDER: '/root/.deploy'
          RUN: 'ls -a; pwd'
  ```
  
## variables 

| variable | example  | require |
| -------- | ----------- | ------- |
| `IP` | `1.1.1.1`| `true` |
| `USER` | `root` | `true` |
| `KEY` | `xxxxxx` | `true` |
| `FOLDER` | `/root/.deploy`| `true` |
| `IGNORE` | `['img.jpg']` | `false` |
| `RUN` | `uptime` | `false` |
