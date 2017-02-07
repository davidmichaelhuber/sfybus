# sfybus
A project which allows easy access to Spotify's D-Bus interface using the command line.

# D-Bus

Find properties and methods of Spotify's D-Bus interface

`dbus-send --print-reply --session --dest=org.mpris.MediaPlayer2.spotify /org/mpris/MediaPlayer2 org.freedesktop.DBus.Introspectable.Introspect`
