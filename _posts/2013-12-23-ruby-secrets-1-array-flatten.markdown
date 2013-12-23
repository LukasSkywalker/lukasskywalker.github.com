---
layout: post
title:  "Ruby secrets #1: Array#flatten"
date:   2013-12-23 13:12:23
---

You probably have at least heard of or even used the [Array#flatten](http://www.ruby-doc.org/core-2.0.0/Array.html#method-i-flatten) method. It returns a flat, one-dimensional copy of the original array:

      > ary = [[1, 2, 3], [3, 4, 5], [4, 5, 6], [7, 8, 9]]
      > ary.flatten
      => [1, 2, 3, 3, 4, 5, 4, 5, 6, 7, 8, 9]
      
Pretty straight-forward, but still a cool feature.

But wait, there's more awesomeness. Array#flatten takes an optional argument that sets the maximum recurstion depth of the flatten calls, making it possible to flatten an array only partially:

    > ary = [[[1, 2], 3], [[3, 4], 5], [[4, 5], 6], [[7, 8], 9]]
    > ary.flatten
    => [1, 2, 3, 3, 4, 5, 4, 5, 6, 7, 8, 9]
    > ary.flatten(1)
    => [[1, 2], 3, [3, 4], 5, [4, 5], 6, [7, 8], 9]
    
As you can see, only the first nesting level of the array is actually flattened.

Now, how is this feature handy? I recently had to display tracking data from a GPS device on a map. The API returned the data as an array of laps, where each lap was an array of waypoints and each waypoint was an array of a latitude and a longitude:

    > track = [[[1.234,5.235],[1.245,5.234],[1.256,5.345]] , [[1.343,5.432],[1.245,5.234]]]
    
This would represent a track with two laps, the first containing three and the second containing two waypoints.
In order to display the track on a map, I needed to get rid of the laps and store the waypoints as a flat array.

Now, instead of doing this:

    > map_data = []
    > track.each { |lap| lap.each { |waypoint| map_data << waypoint } }
    > map_data
    => [[1.234, 5.235], [1.245, 5.234], [1.256, 5.345], [1.343, 5.432], [1.245, 5.234]]
    
I could just run

    > map_data = track.flatten(1)
    => [[1.234, 5.235], [1.245, 5.234], [1.256, 5.345], [1.343, 5.432], [1.245, 5.234]]
    
which is simpler, easier to read and somehow more ruby-ish.