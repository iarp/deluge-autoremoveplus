AutoRemovePlus
==============

AutoRemovePlus is a plugin for [Deluge](http://deluge-torrent.org) that
you can use to automatically remove torrents. It's
based on AutoRemove 0.6.1 by Omar Alvarez, which in turn is based on 0.1 by Jamie Lennox.

This is a Gtk3UI and WebUI plugin. However, since there is not yet any gtk client for wndows for deluge 2.03, this part is currently untested.

New features:
-------------
- First condition is still a minimum, but the second condition is now maximum. Play with these to accomplish what you want
- New option that only applies to finished torrents: pause after hours, and remove after hours.
- Connection to sonarr/lidarr/radarr to blacklist torrent and make the remove through those clients instead. But currently causes http 500 error. Works from command line though.
- Cleaned up the inconsistent times from days and now it's in hours instead.

Features
--------
- Select how many torrents are allowed at the same time.
- Choose to remove or pause them based on multiple criteria age, seeders, seed time or ratio.
- Set specific removal rules depending on tracker or label.
- Remove only torrents from specific trackers or labels.
- Only remove torrents if under a certain HDD space threshold.
- Select if torrents have to fulfill both or either criteria.
- Delete torrents in order (e.g. delete torrents with highest ratio first).
- Don't remove torrents if they don't reach a minimum time (in days) or ratio.
- Choose the removal interval.
- Right click and select torrents that you don't want automatically removed.
- Remove torrent data option.
- Create an exempted tracker or label list, so that torrents that belong to those trackers or labels are not removed.
- Fully functional WebUI.  

Usage
-----
Look for torrents to remove every hour:

> Check every: 1

Remove every torrent that meets minimum criteria:

> Maximum torrents: 0

Don't remove torrents unless Deluge has over 500:

> Maximum torrents: 500

Delete torrents even if HDD space not under minimum:

> Minimum HDD space: -1

Only remove torrents when the main HDD has less than 10 GB free:

> Minimum HDD space: 10

Remove torrents that have an availability under 1.0 and were added 4 days ago or more:

> Remove by: Availability, Min: 1.0, and, Remove by: Age in days, Max: 4  

Remove torrents only according to first criteria:

> :black_small_square: Second Remove by: criteria

Pause torrents instead of removing them:

> :black_small_square: Remove torrents

The rest of the options are pretty self explanatory

Command line usage
------------------
copy mediaserver.py to a folder of your liking and cd to it.

edit /data/server.ini to include the url of your server and api keys for sonarr/radarr/lidarr, can be found under 
settings->general.

syntax:

python3 mediaserver sonarr queue
=> returns sonarr queue

python3 mediaserver radarr delete --item=12345567
> deletes and blacklists that item and returns {} if successful

Building
--------

Run:

```
python setup.py bdist_egg
```

The resulting `AutoRemovePlus-x-py2.x.egg` file can be found in the `/dist` directory.

Workarounds
-----------

If after building the egg file, the plugin does not load in Deluge:

- Delete the `AutoRemovePlus-x-py2.x.egg` in `/deluge/plugins` directory.
- Delete the `AutoRemovePlus.conf` files.
- Restart Deluge.
