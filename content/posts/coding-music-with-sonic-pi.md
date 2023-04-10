---
title: 'Coding Music With Sonic Pi'
date: Sun, 11 Feb 2018 13:19:14 +0000
draft: false
tags: ['music', 'Others', 'sonicpi']
---

Sonic Pi
========

[![](http://www.alvinsim.com/wp-content/uploads/2018/02/sonic-pi-logo-300x292.png)](http://sonic-pi.net)

Lately, I have been playing with [Sonic Pi](http://sonic-pi.net). In a nutshell, it is a music synthesizer. But instead of toggling knobs, switches, keys and what not, we write code. [Ruby](https://en.wikipedia.org/wiki/Ruby_(programming_language)) code to be exact.

Sonic Pi was created by [Sam Aaron](http://twitter.com/samaaron). A bit of history now, if you have not heard of him, he, together with [Johnathan Graham](http://twitter.com/graham_jp), was [Meta-eX](http://www.meta-ex.com). They performed live coding music. Besides that, they also did tech talks to promote coding and music to different groups of people. Do checkout their performances, talks and also music at the Meta-eX website.

Playing with Sonic Pi
=====================

Now, back to Sonic Pi. As I was saying, I played with it these past few weeks over the weekend. After going through the tutorials and examples, I started making music with it.

Here is a glimpse on how to play sound using Sonic Pi.

Do note, if you do not know, the `#` character is for [code commenting or remarks](https://en.wikipedia.org/wiki/Comment_(computer_programming)).

```
# To make a sound or play a note

play 70

# or

play :C4

# This plays the middle "C" note.

# To play, for example, the C chord

play 60
play 64
play 67

# or

play chord(:C, :major)

# To play sound continously, or in a loop

loop do
    play :C4
    sleep 1
end 
```

Sonic Pi also has a number of `fx` and samples you can play with.

To hear how Sonic Pi sounds like, go to [the website](http://sonic-pi.net) and scroll down to "Music. Code. Simple" section. There you can click on the big "Play" button to listen to sounds generated from the code on the left.

My first "Sonic Pi" song was the intro to [Guns N' Roses' Sweet Child O' Mine](https://www.youtube.com/watch?v=1w7OgIMMRc4).

\[audio mp3="http://www.alvinsim.com/wp-content/uploads/2018/02/sweet-child-of-mine.mp3"\]\[/audio\]

You can refer to the source code for this song below, or check-it-out in [my github repo](https://github.com/alvinsim/sonic-pi-songs).

```
with_fx :distortion do
  with_fx :reverb do
    live_loop :intro do
      use_synth :pluck
      play :D3
      sleep 0.25
      play :D4
      sleep 0.25
      play :A3
      sleep 0.25
      play :E3
      sleep 0.25
      play :G4
      sleep 0.25
      play :D3
      sleep 0.25
      play :FS4
      sleep 0.25
      play :D3
      sleep 0.25
    end
  end
end

sleep 4

with_fx :wobble do
  with_fx :reverb do
    live_loop :bass do
      use_synth :chipbass
      2.times do
        play [:A3, :D2]
        sleep 2
      end
      2.times do
        play [:C3, :G3]
        sleep 2
      end
      2.times do
        play [:G2, :D3]
        sleep 2
      end
      2.times do
        play [:A3, :D2]
        sleep 2
      end
    end
  end
end

sleep 16

live_loop :drum_bass do
  sample :drum_heavy_kick
  sleep 2
end

live_loop :drum_cymbal do
  sample :drum_cymbal_pedal
  sleep 2
end

sleep 16

live_loop :drum_tom do
  2.times do
    sample :drum_tom_lo_hard
    sleep 0.25
  end
  sleep 1.5
end 
```

It sounds a bit rough. But I am still learning. So, all the code above generated that 1 minute or so song.

Summary
=======

Sonic Pi is a good platform for everyone, children and adults alike, to learn about music and also writing code. Those who have no experience in writing code can use Sonic Pi to learn the fundamentals of software development e.g. code blocks, iterations, conditionals, functions, variables, etc. These are covered also in the "Help" section - "5. Programming Structures".

Go ahead. Download and install Sonic Pi. It supports Windows, Linux, Mac OS, and Raspberry Pi.

If you like it, do support Sam Aaron at his [Patreon page](https://www.patreon.com/samaaron).

–