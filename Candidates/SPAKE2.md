First the auxiliary questions:

 SPAKE2 is a balanced PAKE. Both peers could initiate at the same time
 but must distinguish their roles somehow. It can be integrated into
 IKEv2 or the TLS handshake. There are per-group parameters: this is
 not a barrier to agility as a method for their generation is
 specified. There is no limit on applicability. The security model is
 not unusual and there are no problems with the proof. As for the
 security with common password entropy the standard security
 requirement for PAKE requires online guessing attempts equal in number
 to the number of passwords guessed. Clearly no scheme can do better,
 and as SPAKE2 has this property it is only as unsafe for common
 passwords as any scheme would have to be.

 SPAKE2 does not have a trusted setup: it does have two system
 parameters which are points of which of the discrete logs would lead
 to a security issue for any exchanges in the future. Any such
 computation would cast significant doubt on the difficulty of the
 discrete logarithm problem in the group. The protocol is 1 round.
 Password hashing guidance does not seem to differentiate PAKE
 protocols. It could of course be included in any document. The same
 for blocking user enumeration: the obvious trick is to use a random
 string as password and continue the PAKE.

 Now the main ones:

* R1: It is a balanced PAKE

* R2:
   There is a security proof in
   Abdalla, M. and D. Pointcheval, "Simple Password-Based
   Encrypted Key Exchange Protocols.", Feb 2005.
   Appears in A. Menezes, editor. Topics in Cryptography-
   CT-RSA 2005, Volume 3376 of Lecture Notes in Computer
   Science, pages 191-208, San Francisco, CA, US. Springer-
   Verlag, Berlin, Germany.

 in the ROM.

* R3: There are no operations that pose any difficulty in rendering
   constant time implementations

* R4: Irrelevant: there is no map in the scheme of the type discussed in RFC 8125.

* R5:
   Each party conducts 4 point multiplications in the course of the
   protocol. Note that two of the multiplications may be combined into
   one computation of x*A+y*B which is moderately more efficient.

* R6:
   I am not sure I understand what R6 is supposed to mean.

* R7:
   Shielding identities is a difficult topic and very protocol specific.

* R8: I am unaware of any patents that bear on SPAKE2.

