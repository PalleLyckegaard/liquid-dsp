
liquid-dsp
==========

Software-Defined Radio Digital Signal Processing Library -
[https://liquidsdr.org](https://liquidsdr.org)

[![Build Status](https://travis-ci.org/jgaeddert/liquid-dsp.svg?branch=master)](https://travis-ci.org/jgaeddert/liquid-dsp)
[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg?style=flat)](https://choosealicense.com/licenses/mit/)

liquid-dsp is a free and open-source digital signal processing (DSP)
library designed specifically for software-defined radios on embedded
platforms. The aim is to provide a lightweight DSP library that does not
rely on a myriad of external dependencies or proprietary and otherwise
cumbersome frameworks. All signal processing elements are designed to be
flexible, scalable, and dynamic, including filters, filter design,
oscillators, modems, synchronizers, complex mathematical operations, and
much more.

For more information, please refer to the
[documentation](https://liquidsdr.org/doc) online.

Installation and Dependencies
-----------------------------

liquid-dsp only relies on `libc` and `libm` (standard C and math)
libraries to run; however liquid will take advantage of other libraries
(such as [FFTW](http://www.fftw.org)) if they are available.

If you build from the Git repository you will also need to install autotools
for generating the `configure.sh` script (e.g.
`brew install autoconf automake` on macOS,
`sudo apt-get install automake autoconf` on Debian variants).

### Installation ###

The recommended way to obtain the source code is to clone the entire
[repository](https://github.com/jgaeddert/liquid-dsp) from
[GitHub](https://github.com):
        
    git clone git://github.com/jgaeddert/liquid-dsp.git

Building and installing the main library is a simple as

    ./bootstrap.sh
    ./configure
    make
    sudo make install

If you are installing on Linux for the first time, you will also need
to rebind your dynamic libraries with `sudo ldconfig` to make the
shared object available.
This is not necessary on macOS.

If you decide that you want to remove the installed DSP library, simply
run

    sudo make uninstall

Seriously, I won't be offended.

### Run all test scripts ###

Source code validation is a critical step in any software library,
particulary for verifying the portability of code to different
processors and platforms. Packaged with liquid-dsp are a number of
automatic test scripts to validate the correctness of the source code.
The test scripts are located under each module's `tests/` directory and
take the form of a C source file. liquid includes a framework for
compiling, linking, and running the tests, and can be invoked with the
make target `check`, viz.

    make check

There are currently more than 90,000 checks to verify functional correctness.
Drop me a line if these aren't running on your platform.

### Examples ###

Nearly all signal processing elements have a corresponding example in
the `examples/` directory.  Most example scripts generate an output
`.m` file for plotting with [GNU octave](https://www.gnu.org/software/octave/)
All examples are built as stand-alone programs and can be compiled with
the make target `examples`:

    make examples

Sometimes, however, it is useful to build one example individually.
This can be accomplished by directly targeting its binary
(e.g. `make examples/modem_example`). The example then can be run at the
command line, viz. `./examples/modem_example`.

### Benchmarking tool ###

Packaged with liquid are benchmarks to determine the speed each signal
processing element can run on your machine. Initially the tool provides
an estimate of the processor's clock frequency and will then estimate
the number of trials so that each benchmark will take between 50 and
500 ms to run. You can build and run the benchmark program with the
following command:

    make bench

Available Modules
-----------------

  * _agc_: automatic gain control, received signal strength
  * _audio_: source audio encoders/decoders: cvsd, filterbanks
  * _buffer_: internal buffering, circular/static, ports (threaded)
  * _channel_: additive noise, multi-path fading, carrier phase/frequency
        offsets, timing phase/rate offsets
  * _dotprod_: inner dot products (real, complex), vector sum of squares
  * _equalization_: adaptive equalizers: least mean-squares, recursive
        least squares, semi-blind
  * _fec_: basic forward error correction codes including several
        Hamming codes, single error correction/double error detection,
        Golay block code, as well as several checksums and cyclic
        redundancy checks, interleaving, soft decoding
  * _fft_: fast Fourier transforms (arbitrary length), discrete sin/cos
        transforms
  * _filter_: finite/infinite impulse response, polyphase, hilbert,
        interpolation, decimation, filter design, resampling, symbol
        timing recovery
  * _framing_: flexible framing structures for amazingly easy packet
        software radio; dynamically adjust modulation and coding on the
        fly with single- and multi-carrier framing structures
  * _math_: transcendental functions not in the C standard library
        (gamma, besseli, etc.), polynomial operations (curve-fitting,
        root-finding, etc.)
  * _matrix_: basic math, LU/QR/Cholesky factorization, inversion,
        Gauss elimination, Gram-Schmidt decomposition, linear solver,
        sparse matrix representation
  * _modem_: modulate, demodulate, PSK, differential PSK, QAM, optimal
        QAM, as well as analog and non-linear digital modulations GMSK)
  * _multichannel_: filterbank channelizers, OFDM
  * _nco_: numerically-controlled oscillator: mixing, frequency
        synthesis, phase-locked loops
  * _optim_: (non-linear optimization) Newton-Raphson, evoluationary
        algorithms, gradient descent, line search
  * _quantization_: analog/digital converters, compression/expansion
  * _random_: (random number generators) uniform, exponential, gamma,
        Nakagami-m, Gauss, Rice-K, Weibull
  * _sequence_: linear feedback shift registers, complementary codes,
        maximal-length sequences
  * _utility_: useful miscellany, mostly bit manipulation (shifting,
        packing, and unpacking of arrays)
  * _vector_: generic vector operations

### License ###

liquid projects are released under the X11/MIT license.
Short version: this code is copyrighted to me (Joseph D. Gaeddert),
I give you full permission to do wantever you want with it except remove my
name from the credits.
Seriously, go nuts.
See the LICENSE file or
[https://opensource.org/licenses/MIT](https://opensource.org/licenses/MIT)
for specific terms.

