# :butterfly: Hyperaudio Lite :butterfly:

:high_brightness: To make media on the web more accessible we believe that every piece of spoken-word audio and video should come with an Interactive Transcript.:high_brightness:

Hyperaudio Lite - is an [Interactive Transcript](https://en.wikipedia.org/wiki/Interactive_transcripts) Viewer

You can use Hyperaudio Lite to provide Interactive Transcripts, this readme details why and how.

- lightweight (less than 8Kb minified)
- no framework dependencies
- MIT Licensed

## :tiger: Hyperaudio Lite in the Wild :tiger:

As demonstrated here [https://hyperaud.io/lab/halite/v28/](https://hyperaud.io/lab/halite/v28/) plus equivalent [multiplayer version](https://hyperaud.io/lab/halite/v28/multiplayer.html)

Alternatively styled version [https://lab.hyperaud.io/mozfest2021/interviews/lance_weiler/](https://lab.hyperaud.io/mozfest2021/interviews/lance_weiler/)

YouTube Integration [https://hyperaud.io/lab/halite/v28/youtube.html](https://hyperaud.io/lab/halite/v28/youtube.html)

SoundCloud Integration [https://hyperaud.io/lab/halite/v28/soundcloud.html](https://hyperaud.io/lab/halite/v28/soundcloud.html)

Vitorio's version [https://github.com/vitorio/hyperaudio-lite](https://github.com/vitorio/hyperaudio-lite)

## :star2: Hyper Powers :star2:

Interactive transcripts are transcripts with special powers. Hyperaudio's Interactive Transcripts are called Hypertranscripts and are infused with the following hyper-powers:

### :world_map: Navigate

Click on the text to navigate directly to the part of the audio where that word was said.

### :mag_right: Search

Find words and phrases inside your transcript and make your media search-engine friendly.

### :couple_with_heart_woman_woman: Share

Selecting part of a transcript creates a URL with timing data which when shared will take people directly to the corresponding piece of audio where the highlighted words are spoken.

## :vhs: Data Formats :vhs:

Hypertranscripts contain the following data:

- Paragraphs
- Words
- Word start time (`data-m` milliseconds)
- Word duration (`data-d` milliseconds)

That's it!

Here's an example:

```html
<p>
  <span data-m="52890" data-d="0" class="speaker">Alexandra: </span>
  <span data-m="52890" data-d="90">I </span>
  <span data-m="52980" data-d="240">think </span>
  <span data-m="53220" data-d="720">unfortunately </span>
  <span data-m="53970" data-d="60">at </span>
  <span data-m="54030" data-d="60">the </span>
  <span data-m="54090" data-d="270">minute, </span>
  <span data-m="54390" data-d="180">we </span>
  <span data-m="54570" data-d="180">make </span>
  <span data-m="54750" data-d="270">people </span>
  <span data-m="55020" data-d="300">aware </span>
  <span data-m="55320" data-d="90">of </span>
  <span data-m="55410" data-d="150">their </span>
  <span data-m="55560" data-d="480">personal </span>
  <span data-m="56040" data-d="330">data </span>
  <span data-m="56370" data-d="210">when </span>
  <span data-m="56580" data-d="480">terrible </span>
  <span data-m="57060" data-d="300">things </span>
  <span data-m="57360" data-d="510">happen. </span>
</p>
```

Hyperaudio Lite is "tag agnostic" so for example, you could use other tags instead of `<span>` to wrap words.

You could also make headings link to chapter points using attributes, like this:

```html
<h5 data-m="214800">
  What kind of help is available for people to manage their own data?
</h5>
```

We can see that a Hypertranscript is really just HTML, this helps keep it:

- :clap: extensible
- :clap: accessible
- :clap: readable

### How to make a Hypertranscript

One way is to use the [Hyperaudio Converter](https://hyperaud.io/converter/)

This currently takes 4 possible inputs:

- SRT (Subtitle format)
- [Speechmatics](https://www.speechmatics.com/) JSON\*
- [Gentle](https://github.com/lowerquality/gentle) JSON
- [Google Speech-to-Text](https://cloud.google.com/speech-to-text/) JSON

\*JavaScript Object Notation - a common data format

## :floppy_disk: Hyperaudio Lite Code :floppy_disk:

Essentially the Hyperaudio Lite library is made from 4 JavaScript files:

1. `hyperaudio-lite.js` - the core that deals with the linking of media to words
2. `hyperaudio-lite wrapper` - adds search, selection and playback rate functionality
3. `share-this.js` - a fork of [share-this](https://github.com/MaxArt2501/share-this) library
4. `share-this.twitter.js` - a fork of the Twitter sharing element of share-this

and the associated CSS files:

5. `hyperaudio-lite-player.css`
6. `share-this.css`

We also link to [Velocity 1.5](https://github.com/julianshapiro/velocity) for autoscroll and Twitter widget JS for Twitter sharing.

Add to your HTML file in the following way:

```HTML
<head>
  <link rel="stylesheet" href="css/hyperaudio-lite-player.css">
  <script src="https://cdnjs.cloudflare.com/ajax/libs/velocity/1.5.0/velocity.js"></script>
  <script src="https://platform.twitter.com/widgets.js"></script>
</head>
```

and at the end of the `<body>`:

```html
  <script src="js/hyperaudio-lite.js"></script>
  <script src="js/hyperaudio-lite-wrapper.js"></script>
  <script src="js/share-this.js"></script>
  <script src="js/share-this-twitter.js"></script>
  <script>
    ShareThis({
      sharers: [ ShareThisViaTwitter ],
      selector: "article"
    }).init();
  </script>
</body>
```

Finally instantiate the Transcript Player:

```javascript
let minimizedMode = false;
let autoScroll = true;
let doubleClick = false;
let webMonetization = false;

new HyperaudioLite("hypertranscript", "hyperplayer", minimizedMode, autoScroll, doubleClick, webMonetization);
```

View the source code of [http://hyperaud.io/lab/halite/v28/](https://hyperaud.io/lab/halite/v28/) for a complete example.

See a version with multiple players in a single page [http://hyperaud.io/lab/halite/v28/multiplayer.html](https://hyperaud.io/lab/halite/v28/multiplayer.html)

## :tv: YouTube Support :tv:

In addition to supporting the web-native HTML `<audio>` and `<video>` elements we also support a YouTube `iframe` embed.

Example of YouTube `iframe` embed:

```html
<iframe
  id="hyperplayer"
  data-player-type="youtube"
  width="400"
  height="300"
  frameborder="no"
  allow="autoplay"
  src="https://www.youtube.com/embed/xLcsdc823dg?enablejsapi=1"
>
</iframe>
```

## :sound: SoundCloud Support :sound:

We also support a SoundCloud `iframe` embed.

Example of Soundcloud API and `iframe` embed:

```html
<script src="https://w.soundcloud.com/player/api.js"></script>
<iframe
  id="hyperplayer"
  data-player-type="soundcloud"
  width="100%"
  height="166"
  scrolling="no"
  frameborder="no"
  allow="autoplay"
  src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/730479133&color=%23ff5500&auto_play=false&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true"
></iframe>
```

You can get the snippet of code by visiting the page of the SoundCloud file you're interested in, clicking on _Share_ and then _Embed_.


## :money_with_wings: Web Monetization Support :money_with_wings:

[Web Monetization](https://webmonetization.org/) is a JavaScript browser API that allows the creation of a payment stream from the user agent to the website and a [proposed](https://discourse.wicg.io/t/proposal-web-monetization-a-new-revenue-model-for-the-web/3785) [W3C](https://www.w3.org/) standard.

You can use this with Hyperaudio Lite to apportion streaming funds (from viewers with Web Monetization compatible wallets and browser extensions) to different sources depending on the transcript or part of the transcript you are currently listening to.

To activate set the Web Monetization parameter when instantiating a new `HyperaudioLite` object to `true`, for example:

```javascript
let minimizedMode = false;
let autoScroll = true;
let doubleClick = false;
let webMonetization = true;

new HyperaudioLite("hypertranscript", "hyperplayer", minimizedMode, autoScroll, doubleClick, webMonetization);
```

If you then set the `data-wm` attributes in your transcript streaming will be switched to that payment pointer when encountered.

```html
   <article data-wm="$ilp.uphold.com/123article">

      <section data-wm="$ilp.uphold.com/123section">

        <h5 data-m="0">How do we make people more aware of their personal data?</h5>

        <p data-tc="00:00:04" data-wm="$ilp.uphold.com/123Doc">
          <span data-m="4470" data-d="0" class="speaker">Doc: </span>
          <span data-m="4470" data-d="270">We </span>
          <span data-m="4740" data-d="240">have </span>
          <span data-m="5010" data-d="300">two </span>
          <span data-m="5310" data-d="600">selves </span>
          ...
```

*Note* – if a `data-wm` attribute is not present in an element Hyperaudio Lite will check the parent (and parent's parent etc) until it finds one. 

## :construction_worker: Testing :construction_worker:

Currently we use [Jest](https://jestjs.io/) for testing.

Install Jest using yarn:
`yarn add --dev jest`

Or npm:
`npm install --save-dev jest`

To run the tests:
`yarn test` or `npm run test`

Note: If you have issues runing the tests, try a more recent version of node. (node v16.0.0 should work).
