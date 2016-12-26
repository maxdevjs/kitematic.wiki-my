# x-terminal-emulator does not exist

Usually `/usr/bin/x-terminal-emulator` is a symlink to your preferred default terminal emulator. So normal applications can launch the correct terminal.

In your case `/usr/bin/x-terminal-emulator` either:

- is broken
- does not exist
- the linked terminal emulator does not support the `-e` option

On Debian and Ubuntu-based distros, you would execute `sudo update-alternatives --config x-terminal-emulator` and choose the correct link in the UI.

On other distros, you could use `sudo ln -sT <your terminal emulator path> /usr/bin/x-terminal-emulator`.

For some additional information, there is a good answer on stackexchange: http://unix.stackexchange.com/questions/32547/how-to-launch-an-application-with-default-terminal-emulator-on-ubuntu