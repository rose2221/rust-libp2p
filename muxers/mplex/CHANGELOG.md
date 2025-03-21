## 0.43.1

- Rename `MplexConfig` to `Config` for consistency with other crates (see [discussion 2174](https://github.com/libp2p/rust-libp2p/discussions/2174)).
  See [PR 5870](https://github.com/libp2p/rust-libp2p/pull/5870).

## 0.43.0

<!-- Update to libp2p-core v0.43.0 -->

## 0.42.0

<!-- Update to libp2p-swarm v0.45.0 -->

## 0.41.0

- Migrate to `{In,Out}boundConnectionUpgrade` traits.
  See [PR 4695](https://github.com/libp2p/rust-libp2p/pull/4695).

## 0.40.0

- Raise MSRV to 1.65.
  See [PR 3715].

[PR 3715]: https://github.com/libp2p/rust-libp2p/pull/3715

## 0.39.0

- Update to `libp2p-core` `v0.39.0`.

## 0.38.0

- Update to `libp2p-core` `v0.38.0`.

- Update `rust-version` to reflect the actual MSRV: 1.60.0. See [PR 3090].

[PR 3090]: https://github.com/libp2p/rust-libp2p/pull/3090

## 0.37.0

- Bump rand to 0.8 and quickcheck to 1. See [PR 2857].

[PR 2857]: https://github.com/libp2p/rust-libp2p/pull/2857

## 0.36.0

- Update to `libp2p-core` `v0.36.0`

## 0.35.0

- Update to `libp2p-core` `v0.35.0`

## 0.34.0

- `Substream` now implements `AsyncRead` and `AsyncWrite`. See [PR 2706].
- Update to `libp2p-core` `v0.34.0`

[PR 2706]: https://github.com/libp2p/rust-libp2p/pull/2706/

## 0.33.0

- Update to `libp2p-core` `v0.33.0`.

## 0.32.0 [2022-02-22]

- Update to `libp2p-core` `v0.32.0`.

- Update to `parking_lot` `v0.12.0`. See [PR 2463].

[PR 2463]: https://github.com/libp2p/rust-libp2p/pull/2463/

## 0.31.0 [2022-01-27]

- Update dependencies.

- Add `fn set_protocol_name(&mut self, protocol_name: &'static [u8])` to MplexConfig

- Migrate to Rust edition 2021 (see [PR 2339]).

[PR 2339]: https://github.com/libp2p/rust-libp2p/pull/2339

## 0.30.0 [2021-11-01]

- Make default features of `libp2p-core` optional.
  [PR 2181](https://github.com/libp2p/rust-libp2p/pull/2181)
- Update dependencies.

## 0.29.0 [2021-07-12]

- Update dependencies.

- Support stream IDs of up to 60 bit length. See [PR 2094] for details.

[PR 2094]: https://github.com/libp2p/rust-libp2p/pull/2094

## 0.28.0 [2021-03-17]

- Update dependencies.

## 0.27.1 [2021-02-15]

- Update dependencies.

## 0.27.0 [2021-01-12]

- Update dependencies.

## 0.26.0 [2020-12-17]

- Update `libp2p-core`.

## 0.25.0 [2020-11-25]

- Update `libp2p-core`.

- Change the default `split_send_size` from 1KiB to 8KiB.
  [PR 1834](https://github.com/libp2p/rust-libp2p/pull/1834).

## 0.24.0 [2020-11-09]

- Change the default configuration to use `MaxBufferBehaviour::Block`
  and yield from waiting for the next substream or reading from a
  particular substream whenever the current read loop may have
  already filled a substream buffer, to give the current task a
  chance to read from the buffer(s) before the `MaxBufferBehaviour`
  takes effect. This is primarily relevant for
  `MaxBufferBehaviour::ResetStream`.
  [PR 1825](https://github.com/libp2p/rust-libp2p/pull/1825/).

- Tweak the naming in the `MplexConfig` API for better
  consistency with `libp2p-yamux`.
  [PR 1822](https://github.com/libp2p/rust-libp2p/pull/1822).

- Update dependencies.

## 0.23.1 [2020-10-28]

- Be lenient with duplicate `Close` frames received. Version
  `0.23.0` started treating duplicate `Close` frames for a
  substream as a protocol violation. As some libp2p implementations
  seem to occasionally send such frames and it is a harmless
  redundancy, this releases reverts back to the pre-0.23 behaviour
  of ignoring duplicate `Close` frames.

## 0.23.0 [2020-10-16]

- More granular execution of pending flushes, better logging and
  avoiding unnecessary hashing.
  [PR 1785](https://github.com/libp2p/rust-libp2p/pull/1785).

- Split receive buffers per substream.
  [PR 1784](https://github.com/libp2p/rust-libp2p/pull/1784).

- Address a potential stall when reading from substreams.

- Send a `Reset` or `Close` to the remote when a substream is dropped,
  as appropriate for the current state of the substream,
  removing that substream from the tracked open substreams,
  to avoid artificially running into substream limits.

- Change the semantics of the `max_substreams` configuration. Now,
  outbound substream attempts beyond the configured limit are delayed,
  with a task wakeup once an existing substream closes, i.e. the limit
  results in back-pressure for new outbound substreams. New inbound
  substreams beyond the limit are immediately answered with a `Reset`.
  If too many (by some internal threshold) pending frames accumulate,
  e.g. as a result of an aggressive number of inbound substreams being
  opened beyond the configured limit, the connection is closed ("DoS protection").

- Update dependencies.

## 0.22.0 [2020-09-09]

- Bump `libp2p-core` dependency.

## 0.21.0 [2020-08-18]

- Bump `libp2p-core` dependency.

## 0.20.0 [2020-07-01]

- Update `libp2p-core`, i.e. `StreamMuxer::poll_inbound` has been renamed
  to `poll_event` and returns a `StreamMuxerEvent`.

## 0.19.2 [2020-06-22]

- Deprecated method `Multiplex::is_remote_acknowledged` has been removed
  as part of [PR 1616](https://github.com/libp2p/rust-libp2p/pull/1616).

- Updated dependencies.
