
# deck.browsercast.js-demo

Simple demo and development projet for the [browsercast extension (in its own repository)](http://github.com/twitwi/deck.browsercast.js).

There are a few available demo to watch:
- [the browsercast pitch](http://twitwi.github.io/deck.browsercast.js-demo/pitch)
- [a test presentation](http://twitwi.github.io/deck.browsercast.js-demo/)

# Command to re-generate the audio soundtrack from the demo

    echo "deck.browsercast.js is a deck.js extension. It can replay a pre-recorded audio soundtrack and synchronize it with deck.js slides. It also helps in recording the timings and synchronize them with the soundtrack. Thank you very much for your attention." | text2wave | oggenc -o synth.ogg -



# Commands to pack deck.js with everything (used to make gh-pages way faster)

There is a tool coming with some deck.js extensions that will pack all js and css files into a single js file.
Loading is way faster as it diminishes a lot the requests (that are sequential with includedeck).

## The first time

    git checkout gh-pages 
    git merge master
    git checkout master
    
    git clone https://github.com/twitwi/deck.js tmpdeck --depth 5
    node ./tmpdeck/extensions/bundle-maker/make-packed.js "profile-5 browsercast/popcorn.js browsercast/deck.browsercast.js browsercast/deck.browsercast.css browsercast/player.css"
    sed -i -e 's@/home/.*/tmpdeck//*@..../@g' deckjs-custom.js

    git checkout gh-pages
    git add deckjs-custom.js 
    git rm deck.js
    git rm browsercast
    ### + edit and add the pres so they use new stuff
    ### + get the swiss theme for the test demo
    git commit
    git push --all

## To update/merge the gh-pages

### In case of html update (should be commited)

    git checkout gh-pages
    git merge master
    # may need a "git rm browsercast" if browsercast was updated (same for deck.js)
    git checkout master
    git submodule update --init
    git push --all

### In case of browsercast evolution

Probably do that (to be re-tested)

    git checkout master
    git clone https://github.com/twitwi/deck.js tmpdeck --depth 5
    node ./tmpdeck/extensions/bundle-maker/make-packed.js "profile-5 browsercast/popcorn.js browsercast/deck.browsercast.js browsercast/deck.browsercast.css browsercast/player.css" .custom.js
    sed -i -e 's@/home/.*/tmpdeck//*@..../@g' .custom.js
    
    git checkout gh-pages
    mv .custom.js deckjs-custom.js 
    git add deckjs-custom.js 
    git commit -m 'updated custom packed deck.js'
    git push --all
    
    git checkout master
    git submodule update --init
    
