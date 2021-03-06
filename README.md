[![Build Status](https://travis-ci.org/AidosKuneen/glyph.svg?branch=master)](https://travis-ci.org/AidosKuneen/glyph)
[![GoDoc](https://godoc.org/github.com/AidosKuneen/glyph?status.svg)](https://godoc.org/github.com/AidosKuneen/glyph)
[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/AidosKuneen/glyph/master/LICENSE)
[![Coverage Status](https://coveralls.io/repos/github/AidosKuneen/glyph/badge.svg?branch=master)](https://coveralls.io/github/AidosKuneen/glyph?branch=master)

GLYPH 
=====

## Overview

This is an implementation of [GLYPH](https://eprint.iacr.org/2017/766.pdf), which is
a signature scheme based on Ring-LWE. 

This software is mostly a rewrite of a [GLYPH implementation](https://github.com/quantumsafelattices/glyph) in Golang except that:


* The implementation uses different q and B from the papaer for smaller sizes.
(Note that these pramemetrs should also make the crypto more secure)

| | This implementation | In the Paper |
| - | - | -|
| Q | 12289 | 59393 |
|B  | 4095 | 16383 | 
| Bytes of a Public key | 1792 bytes | 2048 bytes |
| Bytes of a Signature | 1942 bytes | 2198 bytes |
| Total | 3734 bytes | 4246 bytes |

The drawback is that we need some time to sign a message (at most a few seconds).

* The implementation uses the NTT algorithm applied in 
[NewHope](https://github.com/Yawning/newhope) for faster FFT.



## Requirements

* git
* go 1.9+

are required to compile.


## Install
    $ go get github.com/AidosKuneen/glyph


## Usage
```go
	message := []byte("some message")

	sk, err := glyph.NewSK()
	sig, err := sk.Sign(message)
	pk := sk.PK()
	err:=pk.Verify(sig, message)
```



## Performance

Using the following test environment...

```
* Compiler: go version go1.10.3 linux/amd64
* Kernel: Linux WS777 4.13.5-1-ARCH #1 SMP PREEMPT Fri Oct 6 09:58:47 CEST 2017 x86_64 GNU/Linux
* CPU:  Celeron(R) CPU G1840 @ 2.80GHz 
* Memory: 8 GB
```


For signing, it takes about 400 mS.

For verification, it takes about 240 uS.

```
BenchmarkSign-2        	      10	 401147645 ns/op
BenchmarkVeri-2        	   10000	    237446 ns/op
```


## Dependencies and Licenses

This software includes a rewrite (from C++ to go)  of https://github.com/quantumsafelattices/glyph,
which is covered by "Unlicense".

This software includes codes from
https://github.com/Yawning/newhope,
which is covered by "CC0 1.0 Universal" license.


```
github.com/AidosKuneen/numcpu  MIT License
Golang Standard Library                       BSD 3-clause License
```