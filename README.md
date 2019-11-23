# keygit
keygit is a Python-based tool that allows version control of keypassx password
stores using git, ensuring that you have always the newest version everywhere.
It adds a layer of symmetric encryption on top of the encrypted KeepassXC file
format using [encdec](https://github.com/johndoe31415/encdec) and
machine-stored keys, which means that you'll have to enter your passphrase once
for every machine in order to be able to (meaningfully) modify the repository
content. In theory, this would allow you to distrust the repository in which
you actually manage the KeepassXC files to the extent that it could be public.
Which it shouldn't be, obviously, but I believe it could.

## Usage
Initial import of a key database. First setup a git repository that you'll use
to manage your key file and have a working remote. E.g.:

```
$ git clone git@myserver.com:keypass
Cloning into 'keypass'...
warning: You appear to have cloned an empty repository.
```

Then, make sure you have the `encdec` tool available and import your current
keypass database:

```
$ ./keygit -e ../encdec/encdec -i pwdb.kdbx ~/keypass/key ~/keypass/db
Master passphrase:
Deriving key, this might take a long time...
Initial key derivation finished after 46.4 seconds.
[master (root-commit) bd51c10] Change on reliant
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 db
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Delta compression using up to 12 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 90.89 KiB | 11.36 MiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To myserver.com:keypass
 * [new branch]      master -> master
```

Subsequently, invoke:

```
$ ./keygit  -e ../encdec/encdec ~/keypass/key ~/keypass/db
```

Which will first pull any updates from the repote, invoke KeepassXC, then
re-encrypt the file if it has changed and re-upload it.

## License
GNU GPL-3.
