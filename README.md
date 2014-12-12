
# deck.browsercast.js-demo

Simple demo and development projet for the browsercast extension.

There are a few available demo to watch:
- [the browsercast pitch](http://twitwi.github.io/deck.browsercast.js-demo/pitch)
- [a test presentation](http://twitwi.github.io/deck.browsercast.js-demo/)

# Command to re-generate the audio soundtrack from the demo

    echo "deck.browsercast.js is a deck.js extension. It can replay a pre-recorded audio soundtrack and synchronize it with deck.js slides. It also helps in recording the timings and synchronize them with the soundtrack. Thank you very much for your attention." | text2wave | oggenc -o synth.ogg -
