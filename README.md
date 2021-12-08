# kaslurp - a REPL wrapper for kaput-cli 

MIT Licence. Copyright 2021. Jay Caines-Gooby jay@gooby.org
https://twitter.com/jaygooby

[`kaput`](https://github.com/davidchalifoux/kaput-cli)
is a [put.io](https://put.io) client.

On my Raspberry Pi, `kaput` is slow to start due
to the limited system resources. `kaslurp`
lets you download multiple put.io files without
needing to restart kaput each time.

More detail in https://jay.gooby.org/2021/12/08/a-repl-wrapper-for-kaput-cli-a-put-io-client

You can make and change the directory the files are saved to,
you can check what existing files you have, from
within the kaslurp REPL and you can also call it to
quickly background download files without needing to
wait for the kaput UI.

```
$ kaslurp
/mnt/video kaslurp> d 123456
Downloading 12345 in the background
/mnt/video kaslurp> cd Thrillers
/mnt/video/Thrillers kaslurp> ls
total 263MB
-rw-r--r-- 1 pi pi 263M Jan  1 21:31 Dressed_to_Kill_(1946).mp4
/mnt/video/Thrillers kaslurp> mkdir "Sherlock Holmes"
/mnt/video/Thrillers kaslurp> cd Sherlock\ Holmes
/mnt/video/Thrillers/Sherlock Holmes kaslurp>
```

By default you'll start with a REPL in your $MEDIADIR
but if you call `kaslurp` like this:

```
kaslurp 123456789
```

it will spawn a background download of the put.io
media id `123456789` saving it to your current `pwd`
and return you to the command line.

If you call it like this:

```
kaslurp -d /tmp 123456789
```

It will first `cd` to `/tmp` and background download the
the file there.

You can also override the starting `MEDIADIR` location
by calling like this:

```
kaslurp -d /tmp
```

You'll get the REPL but be in `/tmp`.

```
Usage:  kaslurp
                Start the REPL

        kaslurp -d /some/path
                Start the REPL at /some/path

        kaslurp <put.io file ID>
                Start a background download of <ID> to your current pwd and exit

        kaslurp -d /some/path <put.io file ID>
                Start a background download of <ID> to /some/path and exit
```        
