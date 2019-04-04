# keygit
keygit is a Python-based tool that allows version control of keypassx password
stores using git, ensuring that you have always the newest version everywhere.
It adds a layer of symmetric encryption on top of the encrypted keepass file
format using [encdec](https://github.com/johndoe31415/encdec) and
machine-stored keys, which means that you'll have to enter your passphrase once
for every machine in order to be able to (meaningfully) modify the repository
content. In theory, this would allow you to distrust the repository in which
you actually manage the keepassx files to the extent that it could be public.
Which it shouldn't be, obviously, but I believe it could.

## License
GNU GPL-3.
