# A cycle between `curl` and `curl-sys`

I'm on debian, building from the debian-packaged rust curl crates.

In particular, i've got `librust-curl-dev` installed, and as you can see the local `.cargo/config.toml` points to the debian repo.

but with this project, when i `cargo build`, both `curl` and `curl-sys` get rebuilt each time.

I think this is due to `curl` getting rebuilt whenever `curl-sys` gets rebuilt, and `curl-sys` getting rebuilt whenever `curl` gets rebuilt (see https://github.com/alexcrichton/curl-rust/pull/407)

```bash
0 dkg@alice:~/src/rust/curl-cycle$ cargo build
   Compiling curl-sys v0.4.49+curl-7.79.1
   Compiling curl v0.4.39
   Compiling curl-cycles v0.0.1 (/home/dkg/src/rust/curl-cycle)
    Finished dev [unoptimized + debuginfo] target(s) in 2.42s
0 dkg@alice:~/src/rust/curl-cycle$ cargo build
   Compiling curl-sys v0.4.49+curl-7.79.1
   Compiling curl v0.4.39
   Compiling curl-cycles v0.0.1 (/home/dkg/src/rust/curl-cycle)
    Finished dev [unoptimized + debuginfo] target(s) in 2.48s
0 dkg@alice:~/src/rust/curl-cycle$ 
```
