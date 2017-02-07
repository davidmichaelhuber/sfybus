# sfybus
A project which allows easy access to Spotify's D-Bus interface using the command line.

# D-Bus

Find properties and methods of Spotify's D-Bus interface:

`dbus-send --print-reply --session --dest=org.mpris.MediaPlayer2.spotify /org/mpris/MediaPlayer2 org.freedesktop.DBus.Introspectable.Introspect`

... will return this:

```xml
<!DOCTYPE node PUBLIC "-//freedesktop//DTD D-BUS Object Introspection 1.0//EN"
                      "http://www.freedesktop.org/standards/dbus/1.0/introspect.dtd">
<!-- GDBus 2.48.1 -->
<node>
  <interface name="org.freedesktop.DBus.Properties">
    <method name="Get">
      <arg type="s" name="interface_name" direction="in"/>
      <arg type="s" name="property_name" direction="in"/>
      <arg type="v" name="value" direction="out"/>
    </method>
    <method name="GetAll">
      <arg type="s" name="interface_name" direction="in"/>
      <arg type="a{sv}" name="properties" direction="out"/>
    </method>
    <method name="Set">
      <arg type="s" name="interface_name" direction="in"/>
      <arg type="s" name="property_name" direction="in"/>
      <arg type="v" name="value" direction="in"/>
    </method>
    <signal name="PropertiesChanged">
      <arg type="s" name="interface_name"/>
      <arg type="a{sv}" name="changed_properties"/>
      <arg type="as" name="invalidated_properties"/>
    </signal>
  </interface>
  <interface name="org.freedesktop.DBus.Introspectable">
    <method name="Introspect">
      <arg type="s" name="xml_data" direction="out"/>
    </method>
  </interface>
  <interface name="org.freedesktop.DBus.Peer">
    <method name="Ping"/>
    <method name="GetMachineId">
      <arg type="s" name="machine_uuid" direction="out"/>
    </method>
  </interface>
  <interface name="org.mpris.MediaPlayer2">
    <method name="Raise"/>
    <method name="Quit"/>
    <property type="b" name="CanQuit" access="read"/>
    <property type="b" name="CanRaise" access="read"/>
    <property type="b" name="HasTrackList" access="read"/>
    <property type="s" name="Identity" access="read"/>
    <property type="s" name="DesktopEntry" access="read"/>
    <property type="as" name="SupportedUriSchemes" access="read"/>
    <property type="as" name="SupportedMimeTypes" access="read"/>
  </interface>
  <interface name="org.mpris.MediaPlayer2.Player">
    <method name="Next"/>
    <method name="Previous"/>
    <method name="Pause"/>
    <method name="PlayPause"/>
    <method name="Stop"/>
    <method name="Play"/>
    <method name="Seek">
      <arg type="x" name="Offset" direction="in"/>
    </method>
    <method name="SetPosition">
      <arg type="o" name="TrackId" direction="in"/>
      <arg type="x" name="Position" direction="in"/>
    </method>
    <method name="OpenUri">
      <arg type="s" name="Uri" direction="in"/>
    </method>
    <signal name="Seeked">
      <arg type="x" name="Position"/>
    </signal>
    <property type="s" name="PlaybackStatus" access="read"/>
    <property type="s" name="LoopStatus" access="readwrite"/>
    <property type="d" name="Rate" access="readwrite"/>
    <property type="b" name="Shuffle" access="readwrite"/>
    <property type="a{sv}" name="Metadata" access="read"/>
    <property type="d" name="Volume" access="readwrite"/>
    <property type="x" name="Position" access="read"/>
    <property type="d" name="MinimumRate" access="read"/>
    <property type="d" name="MaximumRate" access="read"/>
    <property type="b" name="CanGoNext" access="read"/>
    <property type="b" name="CanGoPrevious" access="read"/>
    <property type="b" name="CanPlay" access="read"/>
    <property type="b" name="CanPause" access="read"/>
    <property type="b" name="CanSeek" access="read"/>
    <property type="b" name="CanControl" access="read"/>
  </interface>
</node>
```

The following command is used to read the `Metadata` property. The returned XML by the introspection needs to be used to find the correct syntax for such commands.

`dbus-send --print-reply --session --dest=org.mpris.MediaPlayer2.spotify /org/mpris/MediaPlayer2 org.freedesktop.DBus.Properties.Get string:'org.mpris.MediaPlayer2.Player' string:'Metadata`
