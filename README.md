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

