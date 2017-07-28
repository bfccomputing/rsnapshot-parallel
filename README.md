# rsnapshot-parallel
Run rsnapshot jobs in parallel for much greater performance.

## Description
rsync will not fully utilize your backup disk speed, thereby making your backups take 2-3 times longer than they should.  Parallel rsync works just fine to keep your disks busy.

This is a script that works based off a single rsnapshot.conf file.  It handles making jobs for each host defined in the config file and sets up a crontab to run them in sequence, probably overlaping in time (you can tune the JOB_INTERVAL to make that happen).

It understands simple rsnapshot configurations like this:

```
backup  backup@repo:/.        repo/    +rsync_long_args=--whole-file
backup  backup@repo:/boot/.   repo/    +rsync_long_args=--whole-file
```

The cronjob order will be based on the order in ```/etc/rsnapshot.conf```.  Currently this will only build a 'daily' cronjob.  It could be extended to do more intervals but here we're using filesystem-level snapshotting now so we don't need that.

The script will try to kill existing rsnapshot and rsync processes before it begins.

You might want to run it with the 'bomb' mode if you need a massive immediate backup.
This is very likely to saturate your IO bandwidth, and maybe that's what you want.

## Author
Bill McGonigle <bill@bfccomputing.com>

## License
WTFPL 2.0

## Blog post
Read our [blog post](https://www.bfccomputing.com/2017/07/28/rsnapshot-parallel.html) about the release.
