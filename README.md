# KeyCase Spec

## Purpose

The purpose of this project is to fork and create an open source implementation of Keybase.

## Status

Currently the KeyBase client is [open source](https://github.com/keybase/client) (Go, ReactNative) but the server is proprietary.  [KeyBase server API is documented](https://keybase.io/docs/api/1.0), but it's uncertain whether undocumented endpoints exist which may be crucial for the app's functionality.

## Roadmap

1. Modify the client code to record all request/response data.  Walk through important workflows and capture example traffic.
2. Prioritize what we would like in an MVP.  Decide what technologies to use for the server.
3. Implement server side for the MVP.  Test with (relatively unmodified) client.
4. Trim down the client and eliminate features that aren't in the MVP.
5. Now we have a focused client + server that may be maintainable by small team/small budget.

Then:
* Should we reimplement the client in Rust, Flutter, etc?
* Consider Holochain integration?
* Pursue funding, allies?
* Add features with some use case in mind?
* Is it useful to implement mirroring of the original Keybase server?


