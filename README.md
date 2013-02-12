BandsInTown Playlister
======================

This is simply an experiment to stitch together the BandsInTown API to
get local bands playing during the current day, and then searching for
the top songs by each band. Ideally, I'd like to get to a point where I
can use the Rdio or Grooveshark streaming API's to generate a daily
playlist via a simple webapp.

Currently, there are two rake tasks where I'm experimenting with the
Rdio and BandsInTown API's. Right now, it's only using public API's, but
I'll need to figure out OAuth before I can start streaming songs.

A good intermediate solution might be to link to the Top Song playlists
for each artist.

If I decide to filter by genre, I don't think BandsInTown nor Rdio
accomodates this, but it seems that the EchoNest API is the official
recommendation of Rdio:

https://groups.google.com/d/msg/rdio-api/s2qFx4cRhfI/5HZTbCM-URkJ

Requirements
------------

- An Rdio application client key and secret, which are creatable on-demand and for
free through their developer portal: http://developer.rdio.com/

I'm keeping my credentials in a gitignored `.rdio_credentials` file,
which I'm simply sourcing to export them into the current terminal
session:

    source .rdio_credentials

There is a sample in the repo that can be renamed and editted after
you've created a free Rdio application via their portal.
