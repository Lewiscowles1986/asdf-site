# ASDF site with DarkMode

ASDF site was too bright. Turns out they have a wider set of goals.

This is a spike to see about attaining some goals.

## Building a local copy

```shell
git clone https://github.com/Lewiscowles1986/asdf-site.git
docker run --rm -it \
    -v $(pwd)/asdf-site:/srv/jekyll jekyll/jekyll bash -lc 'bundle install && bundle exec jekyll build .'
    && cd asdf-site/_site && python3 -m http.server && cd ../..
```

### Running

From within the repo this seems to be possible

```shell
docker run --rm -it -v $(pwd):/srv/jekyll -p 8000:4000 --user 1000:1000 jekyll/jekyll bash -lc 'bundle install && bundle exec jekyll serve --host 0.0.0.0 --force-polling --livereload --watch .'
```

If you want to run locally, you must either install webrick gem outside of bundling, or `bundle add webrick` for Jekyll to work on newer ruby versions. This is now enabled in this repo by default.

The use of python is optional. Any software that can serve should be good enough. Also build could become serve, and a port-map used to get this to expose docker port; it's just more complexity than mouting a filesystem.

## Unsolved issues

* search is there, but crap & manual.
* remote sources are not imported feels like it should be a CI task with a default file comitted for each.
* There was no regression test suite so some things may be missing.
* screen noticeably flashes on load with non-default theme and on change. Re-flow & non-async.
* tweaks may be needed to make it more usable for others.

## Main focuses

* Dark mode.
* Theme switching.
* Accessibility (keyboard nav).
* Not changing DOM or layout.
* Integrating syntax highlighter.

## Apologies

* Git History
* Separate repo
* if it works, ship it code (I did two spikes, one with the generation tool you use now...)
* Running docker as root. Unfortunately I didn't want to also debug `jekyll/jekyll`, `--user 1000:1000` didn't seem to work
