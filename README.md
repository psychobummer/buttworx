![foo](./assets/shot.png)

### What is Buttworx?

Buttworx is PsychoBummer's entirely over-engineered answer to the question: 
> "How can I use my drum machine to control thousands of buttplugs distributed across the planet?"

### How does this work?

Simple. We created [pbrelay](https://github.com/psychobummer/pbrelay), a generic gRPC-based `producer->subscriber` streaming framework, which allows a producer to stream (optionally signed) messages to an arbitrary number of subscribers. These messages can, in turn, be used with [buttwork](https://github.com/psychobummer/buttwork), our unified driver for a number of the most popular bluetooth-enabled sex toys.

### So how do I use my drum machine to control sex toys?

[pbrelay-producer](https://github.com/psychobummer/pbrelay-producer) will allow you to listen on a local MIDI port/channel and stream those messages into `pbrelay`.
[pbrelay-subscriber](https://github.com/psychobummer/pbrelay-subscriber) will allow those pbrelay-consumed MIDI messages to control a local BTLE vibrator.

### How much latency is there?

In our testing, even when validating `ed25519` signatures, there's effectively zero latency on top of network latency. We were able to use Ableton Live to control vibrators on different parts of the continent with no perceptible delay or de-synchronization. A network connection with < 150ms of latency should be "good enough."


### Is this secure?

When a producer starts a stream, `pbrelay` generates an ephemeral private and public [ed25519](https://en.wikipedia.org/wiki/EdDSA) signing key for that stream. `pbrelay` gives the private key to the producer, and stores the public key in its internal repository. When a subscriber connects to a producer stream, their client fetches this public key and uses it to validate the integrity of every message from the producer. All of these connections can themselves be wrapped in TLS. Unless the NSA, GRU or Mossad really want to screw with you, it's probably secure enough. We're absolutely open to analysis or additional contribution, though.

### Is this anonymous?

Yes. No information is shared between the producer and the subscriber. In fact, `pbrelay` provides no discovery mechanism whatsoever. A producer is required to deliver their stream id to subscribers out of band. How they do that is entirely up to them: tweet, skywriting, noosphere. We recommend everyone run their own private numbers station.

### Can you give me a shorter version?

* [pbrelay](https://github.com/psychobummer/pbrelay) provides a way to stream messages from producers to subscribers
* [pbrelay-producer](https://github.com/psychobummer/pbrelay-producer) allows you to publish messages into `pbrelay`
* [pbrelay-subscriber](https://github.com/psychobummer/pbrelay-subscriber) allows you to consume from `pbrelay`
* [buttwork](https://github.com/psychobummer/buttwork) is a unified driver for BTLE sex toys
### Aren't you a record label?

What are you, a cop?