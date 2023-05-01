# Troubleshooting - Failed to allocate directory watch: Too many open files

## Solution

* Check limits with `sysctl fs.inotify`
* Add file `/etc/sysctl.d/60-fs-inotify.conf` :

```
fs.inotify.max_queued_events = 32768
fs.inotify.max_user_instances = 512
fs.inotify.max_user_watches = 524288
```

* Reload with `sudo sysctl --system`


## References

* https://blog.differentpla.net/blog/2022/12/14/failed-allocate-directory-watch/
* See also `/etc/systemd/system.conf` and `/etc/systemd/user.conf` :

```
DefaultLimitNOFILE=4096:524288
```

