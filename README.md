# About
[`audacity-bridge`](audacity-bridge) is a command-line interface for Audacity
with the [`mod-script-pipe` module][scripting] installed and enabled. Unlike
the `mod-script-pipe` module, which only creates two communication pipes at
Audacity startup, the `audacity-bridge` script also handles starting up and
shutting down Audacity, which makes it useful for incorporating Audacity into
batch scripts and `make` recipes.

The [`aupexport`](aupexport) script converts AUdacity Project (AUP) files to
any audio file format understood by Audacity; it also showcases the use of the
`audacity-bridge` script.

[scripting]: http://manual.audacityteam.org/o/man/scripting.html "Scripting – Audacity Manual"

# Known Issues
1. Although the `audacity-bridge` script operates without user intervention, it
   isn't headless – i.e. a running X server is still required on unices.
2. The `mod-script-pipe` interface is _blind_ and therefore brittle. Suppose a
   modal dialogue pops up, when Audacity starts up (f.ex. an orphaned files
   warning).  This dialogue prevents the project file from being loaded, but
   the `audacity-bridge` client has limited means of detecting this.
3. While the Audacity splash screen is displayed, incoming messages are silently
   gobbled. This is handled by adding a [fixed sleep](audacity-bridge#L41) at
   the beginning of the script, but this solution is brittle.
4. Upon receiving the Exit MenuCommand, Audacity crashes at Linux. The
   `audacity-bridge` script [handles this internally](audacity-bridge#L61), so
   no action is required on the part of the user.

# License
This script is [released under GNU GPLv3](LICENSE).
