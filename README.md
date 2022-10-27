# SSH Action
A github action to setup ssh key and config in the current environment

# Usage
```
name: ssh command
on: push
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - id: ssh
        uses: mnival/ssh-action@v0.0.1
        with:
        ssh_host: ${{ secrets.SSH_HOST }}
        ssh_user: ${{ secrets.SSH_USER }}
        ssh_key: ${{ secrets.SSH_KEY }}

      - run: ssh ${{ steps.ssh.outputs.ssh_host_alias }} pwd
```

For multiple servers, run the above action multiple times
```
name: ssh command
on: push
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - id: ssh-foo
        uses: mnival/ssh-action@v0.0.1
        with:
        ssh_host: ${{ secrets.SSH_FOO_HOST }}
        ssh_user: ${{ secrets.SSH_FOO_USER }}
        ssh_key: ${{ secrets.SSH_FOO_KEY }}

      - id: ssh-bar
        uses: mnival/ssh-action@v0.0.1
        with:
        ssh_host: ${{ secrets.SSH_BAR_HOST }}
        ssh_user: ${{ secrets.SSH_BAR_USER }}
        ssh_key: ${{ secrets.SSH_BAR_KEY }}

      - run: ssh ${{ steps.ssh-foo.outputs.ssh_host_alias }} pwd
      - run: ssh ${{ steps.ssh-bar.outputs.ssh_host_alias }} pwd
```
