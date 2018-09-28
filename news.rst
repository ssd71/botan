Release Notes
========================================

Changes between 2.4.0 and 2.4.0-RSCS1, 2018-09-28
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* XMSS signature verification did not check that the signature was of
  the expected length which could lead to a crash. (GH #1537)

* Fix error in certificate wildcard matching (CVE-2018-9127), where a
  wildcard cert for ``b*.example.com`` would be accepted as a match for
  any host with name ``*b*.example.com`` (GH #1519)

* CVE-2018-9860 Fix a bug decrypting TLS CBC ciphertexts which could
  for a malformed ciphertext cause the decryptor to read and HMAC an
  additional 64K bytes of data which is not part of the record. This
  could cause a crash if the read went into unmapped memory. No
  information leak or out of bounds write occurs.

* Change the name of test vector for TLS CBC padding
  (backport of https://github.com/randombit/botan/commit/c792f9f514be46857dbef1edc765b616bc48c5de

* Improve interoperability with TLS attacker
  (backport of https://github.com/randombit/botan/commit/aa6bca4a149228cc3061a7a357865597da53251c)

* Use a fixed validation time point for X.509 path validation
  tests (backport of https://github.com/randombit/botan/commit/575fdeab778669b83e5c5cc37f584a3cdef554f1)

* Add configure.py option --with-static-analysis: sets compiler flags to
  enable static analysis using clang-analyzer

* Fix two off-by-one errors in point multiplication on elliptic curves

* Add results of PKCS#11 interoperability tests to handbook

Changes between 2.0.1 and 2.0.1-RSCS1, 2017-01-12
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* The PKCS11 module did not require any external dependencies, so it has been enabled by default. The -with-pkcs11 and --without-pkcs11 flags to configure.py have been removed. (GH #837)

* Add OS::run_cpu_instruction_probe for runtime probing of ISA extensions. Supporting this requires system-specific techniques, currently Windows SEH and Unix signal handling are supported.

* Add support for ARM NEON in the SIMD_4x32 type

* Add support for ARM CPU feature detection using getauxval (GH #843)

* Fix portability or build problems affecting Sun Studio compiler (GH #846), Solaris, ppc64le, DragonflyBSD (GH #887)

* Add --with-external-libdir to configure.py (GH #857 fixing #19 #767)

* Add OS::get_high_resolution_clock which returns the best resolution clock available on the system.

* Change OS::get_processor_timestamp to return 0 if no hardware cycle counter is available. Previously it silently fell back on some other clock type.

* Report cycles/byte in the output of botan speed.

* Add speed tests for modular exponentiations and ECC scalar multiplies.

* Add command line util timing_test which enables running timing-based side channel analysis of TLS CBC decryption, ECC scalar multiplies, OAEP decoding, and other operations which are prone to providing an oracle via side channel.

* Make it possible to disable -fstack-protector using a build-time flag. GH #863

* Add tests for TLS DSA ciphersuites, more Noekeon tests, others.

* Avoid a GCC warning that triggered on the public key types (GH #849)

* Fix various warnings flagged by pylint and pyflakes linters in configure.py and botan.py (GH #832 #836 #839)

* Rename python wrapper to botan2.py (GH #847)

* Change name constraint test to use a fixed reference time. Test certs have expired.

* Increase miller-rabin iterations for DSA primes (FIPS-186-4) (GH #881)

* Fix possible ISO 9796-2 padding side channel and add a length check (GH #891)

* In CLI, if system RNG is available prefer it

* Converge on a single side channel silent EC blinded multiply algorithm.
  Uses montgomery ladder with order/2 bits scalar blinding and point randomization
  now by default. (GH #893)
