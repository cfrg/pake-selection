## REQ1: A PAKE scheme MUST clearly state its features regarding balanced/augmented versions.
 Augmented PAKE

## REQ2: A PAKE scheme SHOULD come with a security proof and clearly state its assumptions and models.

 This is based off SPAKE2 which has a security proof in Abdalla, M. and D. Pointcheval, "Simple
 Password-Based Encrypted Key Exchange Protocols.", Feb 2005.
 SPAKE2+ adds one term to the end hash of SPAKE2 (b*v*G). b is the server's ephemeral
 private key and v is derived from the password. Server stores v*G it is assumed that solving the
 DLP to get v is hard. It is assumed a proper KDF is used and it is not possible to generate v
 from the other server data. Client generates v from the password and applies that to b*G. Thus
 SPAKE2+ is a secure aPAKE.

 SPAKE2+EE changes the blinding terms from H(pw, N)*N and H(pw, M)*M to
 hashToPoint(H(pw, N)) and hashToPoint(H(pw, M)) where hashToPoint is Elligator or Shallue-
 Woestijne-Ulas (SWU). Most assume hash to point to be a random oracle. The only issue is
 with uneven distribution from field P to cyclical group size Q. If someone determines this to be a
 problem which I don't think it is, we can fix it by multiplying the point generated from the hash to
 point algorithm by another key based off the password: "H(pw, N2)*hashToPoint(H(pw, N))".
 This only adds two multiplies to the client side and server can do these once (or be given the
 points during registration) and store the points. Since the client is doing a password KDF this
 change should not affect runtime by much.

 BSPAKE adds blind salt to SPAKE2+EE which should be able to use OPQAUE's security proof
 of blind salt. There's also security analysis of blind salt in this
 paper https://eprint.iacr.org/2015/644.pdf. Also note that blind salt only adds precomputation
  security.

## REQ3: The authors SHOULD show how to protect their PAKE scheme

 implementation in hostile environments, particularly, how to
 implement their scheme in constant time to prevent timing
 attacks.

 Elligator or Shallue-Woestijne-Ulas (SWU) can be done in constant time. The only thing is in the
 hash to point. There is an if statement while doing the square root, this should use a conditional
 move to prevent timing attacks. Everything else is standard ECC operations, finite field
 operations, or hashing. Well besides the password KDF but that's pick one without timing
 attacks.

## REQ4: If the PAKE scheme is intended to be used with ECC, the

 authors SHOULD discuss their requirements for a potential
 mapping or define a mapping to be used with the scheme.
 Elligator and Shallue-Woestijne-Ulas (SWU) are good choices. Other hash to point algorithms
 that don't rely on a loop and are constant time should also be fine.

## REQ5: The authors of a PAKE scheme MAY discuss its design choice with regard to performance, i.e., its optimization goals.

 Server can store the blinding points "N" and "M" to minimize computations or store a key that is
 expanded to those and "k3". So either store N, M, k3, and v*G or "k" and v*G. Then with "k"
 derive keys necessary for N, M, and k3.
 Client side the initial blind salt calculation "r*H(pw, serverId, clientId)*G" can be done x=r*H(pw,
 serverId, clientId) (mod cyclical group size) then do one scalar multiply x*G. Also if using
 Ed25519 generate r as 1/(8*random()). This way when you unblind by multiplying by 1/r it is a
 multiple of 8.

 For minimizing RTT, the client can start encrypting after 2 messages (client->server, server- client) and the server after 3 messages (client->server, server->client, client->server). Note, which applies to all PAKEs, either party can encrypt a message with a random key and send that key in their "first" encrypted message to decrease latency due to bandwidth.

## REQ6: The authors of a scheme MAY discuss variations of their scheme that allow the use in special application scenarios. In particular, techniques that facilitate long-term (public) key agreement are encouraged.

 Like all PAKEs you end up hashing a bunch of stuff to get a key. From that key you derive
 verifiers and session keys. The session keys can be used long-term. I may have misunderstood
 the question. Also I'm not technically an author unless you call adding blind salt to SPAKE2+EE
 being an author.

## REQ7: Authors of a scheme MAY discuss special ideas and solutions on privacy protection of its users.

 If user is not found, one could use default values for N, M, k3, and v*G (or k and v*G) because
 there's no way to determine if the same values are used every time. Also the default values
 should be generated from random as to not make a successful exchange.

## REQ8: The authors MUST follow the IRTF IPR policy <https://irtf.org/ipr>.

  I am unaware of any patents on BSPAKE.

* How does it meet the "SHOULD" requirements of RFC 8125? See above.
   * Does it meet "crypto agility" requirements, not fixing any particular primitives and/or
 parameters?
 Works with any ECC curve that works with Elligator and Shallue-Woestijne-Ulas (SWU). For example it works with all NIST P curve but P-224 because its field is not 3 modulo 4.

 * What setting is the PAKE suitable for, which applications does it have?
 + "Peer communication" (where both ends share the same password) or "client-server" (where
 the server does not store the password but only a one-way function of the password)?
 Client-server, but technically all client-server PAKEs can be used as peer communication. It's
 just less efficient.
 + A nomination should specify for which use-cases the protocol is recommended ("PAKE as a
 more-secure replacement for a PSK on a machine-2-machine interface" or "PAKE for securely
 accessing a remote HMI interface server (e.g. a web server) without configured WEB-PKI
 certificates").
 "PAKE for securely accessing a remote HMI interface server (e.g. a web server) without
 configured WEB-PKI certificates."
 + Can two communicating parties initiate the key exchange process at the same time, or must it
 always be the case that only one party can initiate the process?
 Client initiates the process.
+ Is it suitable to be considered as a standalone scheme? Yes?
+ Can it be integrated into IKEv2? TLS Handshake? Any other protocols?
* Is there a publicly available security proof? If yes, Sort of, see REQ2.
+ Are there known problems with the proof? Yes, it's not a legit proof.
    Yes. Only requirement is that the protocol let's you add the aPAKE's session key(s) to the
 protocol's session key(s).
     + Is the considered security model relevant for all applications that PAKE is intended for (e.g., if
 a PAKE is to be used in TLS Handshake, it is important that the TLS adversary model is
 considered for the PAKE)?
 No. It's assumed everyone is malicious and have access to a "slow" quantum computer. If the
 attacker observed a successful PAKE exchange, can solve a DLP in about a minute, and the password is not in the top 10,000 passwords, then it will take over a year to crack the password.
 Also depending on rate limiting you can probably guess 10,000 passwords in under a year by
 just acting like a user. Note most other PAKEs get offline classical computer password cracking
 if you solve just one or two DLPs.
 + Does it allow to be sure in sufficient level of security for common values of password lengths?
 Yes? Like all aPAKEs it depends on weather rate limiting is used and if the server's data is
 taken, then the password KDF. Active attackers can just make online password guesses or stop
 exchanges. PQ attackers need to observe a successful exchange and solve a DLP per
 password guess. Most other PAKEs it's solve one or two DLPs and get offline classical
 computer password cracking. In the case of OPAQUE a PQ attacker doesn't need to observe a
 successful exchange as all the information is given during a normal wrong password guess.
 * Security assessment.
 + Does its security depend on any nontrivial implementation properties? Are they clearly stated
 in the document?
 Hash to point is the only issue. I believe the main issue is with uneven distribution of hash to
 point. There is a remedy in REQ2 (part 3).
 + Does the PAKE have precomputation security (for augmented PAKEs)? Yes.
No.
  + If the PAKE relies on the assumption of a trusted setup - more specifically, the discrete
 logarithm relationship between the two group elements in the system setup MUST be unknown -
 in anticipation of the worst but not impossible scenario, the authors should clearly state the
 security implications when the discrete logarithm relationship becomes known, and the
 subsequent mitigation measures.
  * Performance assessment.
 + What's with the “round efficiency” of the PAKE? In a standard two/multi-party secure
 computation setting, the “round” is defined as a step in which all parties can complete
 operations at the same time without depending on each other. In practice, a 2-round protocol
 could be implemented as 2 flows or 3 flows depending on the application context, but that’s
 more the implementation detail.
 Only 4 messages/"flows" are sent to verify both parties (client->server, server->client, client-server, server->client). The client can start encrypting after 2 messages (client->server, server-
 client) and the server after 3 messages (client->server, server->client, client->server). Server
  verifies the client after 3 messages and client verifies the server after 4 messages.
 + How many operations of each type (scalar multiplications, inversions in finite fields, hash
 calculations etc.) are made by each side?

 Client: 5 scalar multiplications, 6 finite field inversions, 2 point adds, 2 from data to point, 1 finite
 field multiply, 2 hash to point, 1 password KDF, 8 hashes (one of which is ~4 blocks)
 Server: 4 scalar multiplications, 4 finite field inversions, 2 point adds, 2 from data to point, 0
 finite field multiply, 0 hash to point, 0 password KDF, 4 hashes (one of which is ~4 blocks and
 one is optional)
 When the server stores v*G and "k" (vs N, M, k3, and v*G) it adds 2 hash to point, 3 hashes
 (one is optional) to the server.
 * Which recommendations for secure usage can be given?
 + Is it defined how the explicit key confirmation is performed/must be performed externally? Are
 there clear statements whether this procedure is optional or mandatory?
 Either but you save on RTT if it's done during. It is not clear, but to make it clear: it is optional
 but the client should be the first to verify or send encrypt data (with AEAD so the server can
 verify). This is to not let a malicious client from gaining data that they can use for an offline PQ
 attacker.
 + Can any recommendations on using iterated hashing (e.g., with Scrypt) with the PAKE be
 given?
 Argon2 is probably the one to go with. If a good cache hard password KDF comes out, that
 would probably be ideal. This is because cache hard algorithms are harder for GPUs at shorter
 runtimes than memory hard algorithms like Argon2 and scrypt. Also memory hard algorithms
 aren't good for lightweight computers such as wireless routers.
 PBKDF2 should be avoided unless required to be use because of NIST or other regulatory
 requirements. If you do use PBKDF2, be mindful of its footgun. Or use its footgun to make a
 better password KDF ("Parallel PBKDF2").
 + Can any recommendations to avoid a user enumeration attack be given? See REQ7.
