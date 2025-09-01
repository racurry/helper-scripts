# Some helper scripts

## backgroundify
Add a background color to transparent pngs

`./backgroundify path/to/source/images path/to/new/images '#555555'`

Requires ImageMagick

## mkvtomp4
Change mkv containers to mp4

`./mkvtomp4 filename.mkv`
`./mkvtomp4 folder_full_of_mkvs`

Requires ffmpeg

## swap_extension
Change the extension on a directory worth of files.

```
cd dir_full_of_files
swap_extension txt md
```

## vidmerge
Combine a bunch of videos into one mp4.

```
vidmerge vid1 vid2 vid3 output_file_name
```

Requires ffmpeg


## batch_rename
Rename all of the files in a given directory.  Gives them all the same name, plus a single digit.

```
batch_rename directory_name "File name prefix"
```

## folderify
Take a directory of files.  For each file, make a folder of the same name.  Move that file into that folder.

```
folderify directory_name
```

## ccmcps
Manage Claude Code CLI MCP servers - quickly enable/disable them to save context when not needed.

```
ccmcps                         # Show current server status (default)
ccmcps status                  # Show enabled/disabled server status
ccmcps list                    # Show detailed server list (raw claude mcp list output)
ccmcps disable                 # Disable all MCP servers
ccmcps disable server_name     # Disable specific server
ccmcps enable                  # Enable all previously disabled servers
ccmcps enable server_name      # Enable specific server
```

The script automatically backs up server configurations when disabling them (stored in `~/.claude_mcp_backup.json`) so they can be easily restored later with the same settings.

Requires Claude Code CLI (`claude` command)

