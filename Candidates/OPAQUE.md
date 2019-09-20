Below are responses to the list of requirements from RFC 8125 as well as answers to the questions in your email from July 5th as they apply to OPAQUE. I have also posted a new version of the OPAQUE draft https://tools.ietf.org/html/draft-krawczyk-cfrg-opaque-02
From RFC 8125:

## REQ1: A PAKE scheme MUST clearly state its features regarding balanced/augmented versions.

OPAQUE is an augmented PAKE (aPAKE) with security against pre-computation attacks.

## REQ2: A PAKE scheme SHOULD come with a security proof and clearly state its assumptions and models.

A detailed security analysis is presented in the paper (Eurocrypt'2018): https://eprint.iacr.org/2018/163.pdf
Analysis is carried in the Universally Composable model under a stronger security definition that covers pre-computation attacks.
The analysis is carried in the random oracle model under the One-More Diffie-Hellman assumption.

## REQ3: The authors SHOULD show how to protect their PAKE scheme implementation in hostile environments, particularly, how to implement their scheme in constant time to prevent timing attacks.

OPAQUE combines an Oblivious PRF (OPRF) with any KCI-secure key exchange. The implementation of the latter would follow best implementation practices as relate to that particular protocol.
For the OPRF defined in the OPAQUE draft, namely, based on elliptic curves, an operation mapping the password into the curve is needed. This is the most tricky aspect for implementation in terms of choosing the right transform into the curve and avoiding timing attacks.
  Fortunately, these aspects are now being documented in the CFRG document draft-sullivan-cfrg-voprf.

## REQ4: If the PAKE scheme is intended to be used with ECC, the authors SHOULD discuss their requirements for a potential mapping or define a mapping to be used with the scheme.

See response to REQ3.

## REQ5: The authors of a PAKE scheme MAY discuss its design choice with regard to performance, i.e., its optimization goals.

The key exchange part of OPAQUE can be chosen depending on different practical criteria such as performance, code availability,
compatibility with an existing protocol (e.g., TLS, IKE), etc.
The OPRF part can be optimized by the choice of elliptic curve and a

 corresponding mapping into the curve. The OPAQUE draft is written
with multiplicative blinding which improves performance in some cases (as discussed in the draft). Hardening, e.g., via iterated hashing, is offloaded to the client, a significant performance gain for servers in
many cases. (See more on these aspects in questions Q13, Q14 and Q17 below.)

## REQ6: The authors of a scheme MAY discuss variations of their scheme that allow the use in special application scenarios. In particular, techniques that facilitate long-term (public) key agreement are encouraged.

## REQ7: Authors of a scheme MAY discuss special ideas and solutions on privacy protection of its users.

The OPAQUE draft explicitly discusses this issue, particularly in the
context of TLS 1.3 where different mechanisms may be used to provide protection to user information. These include techniques that do not
incur additional messages, e.g., using resumed sessions or a mechanism similar to ESNI draft-ietf-tls-esni, as well as use of TLS 1.3 full
handshake augmented with two OPAQUE messages. This is described in the OPAQUE draft and further elaborated in draft-sullivan-tls-opaque.

## REQ8: The authors MUST follow the IRTF IPR policy <https://irtf.org/ipr>.

The only patent I know of that covers an element discussed in the OPAQUE draft is IBM's patent on HMQV. Using HMQV with OPAQUE is completely optional. It is described in the draft as the most
efficient key-exchange protocol with which OPAQUE can be integrated, but many other protocols (as also described in the draft) can be used.
If there is interest in standardizing OPAQUE with HMQV one can check if a free license of the HMQV patent could be provided for such use.
Additional questions from cfrg email (by Stanislav V. Smyshlyaev) on 7/5/2019:
  Note: Questions are in the same order as in the original email but the numbering is mine.

Q1: How does it meet the "SHOULD" requirements of RFC 8125? See above.

Q2: Does it meet "crypto agility" requirements, not fixing any particular primitives and/or parameters?
OPAQUE is fully modular: It uses any OPRF and any KCI-secure key exchange.

Q3: What setting is the PAKE suitable for, which applications does it have? OPAQUE is an asymmetric/augmented PAKE targeted to the client-server setting. The ultimate goal would be to replace password-over-TLS with the much more secure OPAQUE. In the first stages of deployment, one should target applications that have full control of the user-side ending as opposed to relying on generic web-browser environment. Phone-based and some enterprise applications seem good candidates for deployment (but I am a non-expert in actual deployment of such technology - others will
know better).

Q4: Can two communicating parties initiate the key exchange process at the same time, or must it always be the case that only one party can initiate the process?
This question is relevant to symmetric PAKE not aPAKE where the client is the one to initiate the exchange.

Q5: Is it suitable to be considered as a standalone scheme?
The instantiations with SIGMA and HMQV illustrated in the draft are
a basis for stand-alone schemes. However, if user's account information is to be protected from eavesdroppers then an additional mechanism for accomplishing that is needed.

Q6: Can it be integrated into IKEv2? TLS Handshake? Any other protocols?
Yes! This is one of the attractive properties of OPAQUE. Given its modularity, it can be adapted to work with different key exchange protocols. The OPAQUE draft illustrates this feature for the case of TLS 1.3, with a more extensive treatment in draft-sullivan-tls-opaque. Integration with IKE should not be too hard, particularly given that IKE follows the SIGMA protocol which is well suited for integration.

Q7: Is there a publicly available security proof? If yes, Are there known problems with the proof?
Yes. See answer to REQ2 above. No known problems with the proof.
 Two observations for the expert: First, as noted in the paper, the 2-message case (without explicit client authentication) requires a slight relaxation of the UC SaPAKE functionality (without diminishing security against pre-computation attacks). Second, as noted in the paper using multiplicative blinding raises some technical issues which we are still studying (paper should be available shortly). The current OPAQUE draft obviates these technicalities by including the value vU under the OPRF hash. One aspect of the analysis that can be improved is that the current model assumes static corruptions. Moving away from the random oracle model (with its known limitations when implementing it with actual hash functions) would be good, but improbable at this time.
The OPAQUE draft includes a discussion (under security consideratrions) about the applicability to OPAQUE of the Brown and Gallant [BG04] and Cheon [Cheon06] attacks on the one-more DH assumption. The conclusion is that this attack is not practical in the OPAQUE setting.

Q8: Is the considered security model relevant for all applications that PAKE is intended for (e.g., if a PAKE is to be used in TLS Handshake, it is important that the TLS adversary model is considered for the PAKE)?
OPAQUE assumes composition with a secure key-exchange protocol which is resistant to KCI attacks. Any such protocol can be used with OPAQUE.
TLS 1.3 offers such security as analyzed in different papers and by
different methods. As always, the security of actually deployed
protocols is more complex than their underlying theoretical design and analysis. But as long as one uses and implements correctly the OPRF part of OPAQUE, if native TLS 1.3 mechanisms are used for the rest of the protocol then OPAQUE would be no less secure than TLS (and much more secure in comparison to the password-over-TLS application).

Q9: Does it allow to be sure in sufficient level of security for common values of password lengths?
Password length makes no difference to the security analysis of OPAQUE. Obviously, a low entropy password facilitates only and offline attacks.

Q10: Does its security depend on any nontrivial implementation properties? Are they clearly stated in the document?
Note that the OPAQUE draft is not intended as a full detailed specification but as a general description that explains the different components of the protocol, their interaction, and functionality.
A precise specification from which interoperable implementations can developed will be produced when consensus is reached into the best way to instantiate OPAQUE pieces. Yet, the draft already highlights issues of implementation; it also refers to draft-irtf-cfrg-hash-to-curve and draft-sullivan-cfrg-voprf for the more subtle issues surrounding OPRF implementation.

Q11: Does the PAKE have precomputation security (for augmented PAKEs)?
 Yes.

Q12: Does the PAKE relies on the assumption of a trusted setup
No. It doesn't.

Q13: What's with the "round efficiency" of the PAKE?
I am not sure I understand your definition of "round". I prefer to talk
in terms of number of messages (i.e., flows or flights in TLS
terminology). OPAQUE costs two messages for computing the OPRF and any number of messages as defined for the key exchange in use. In many
cases, e.g., SIGMA, HMQV, these messages can be parallelized resulting
in 2 or 3 messages for the whole protocol (3 is always needed if
explicit client authentication is required). Protecting user account
information can add up to two messages depending the setting.

Q14: How many operations of each type (scalar multiplications, inversions in finite fields, hash calculations etc.) are made by each side?
From the OPAQUE draft:
The computational cost of OPAQUE is determined by the cost of the OPRF, the cost of a regular Diffie-Hellman exchange, and the cost of authenticating such exchange. In our elliptic-curve implementation of
the OPRF, the cost for the client is two exponentiations (one or two of which can be fixed base!) and one hashing-into-curve operation;
for the server, it is just one exponentiation. The cost of a DH exchange
is as usual two exponentiations per party (one of which is fixed-base). Finally, the cost of authentication per party depends on the specific KE
 protocol: it is just 1/6 of an exponentiation with HMQV and it is one signature in the case of SIGMA and TLS 1.3. These instantiations preserve the number of messages (two or three) in the underlying KE protocol except in one of the TLS instantiations where user privacy requires an additional round trip (this can be saved if using a mechanism similar to the proposed ESNI extension {{I-D.ietf-tls-esni}}).

Q15: Which recommendations for secure usage can be given?
Not sure what this refers to. If the above answers do not address this, please let me know.

Q16: Is it defined how the explicit key confirmation is performed/must be performed externally? Are there clear statements whether this procedure is optional or mandatory?
Performing key confirmation is a design choice that may depend on the chosen key exchange protocol and desired properties. The security of OPAQUE as an aPAKE does not depend on a key confirmation step (except if one re-defines aPAKE to necessarily include such step). All the instantiations discussed in the draft (HMQV, SIGMA, TLS 1.3) already provide or can be augmented to provide key confirmation.

Q17: Can any recommendations on using iterated hashing (e.g., with Scrypt) with the PAKE be given?
The OPAQUE draft touches on this issue (sections 2.1 and 3.4). The hardening operations are performed by the client. This has the advantage of freeing busy servers from doing this purposely-expensive operation. While most clients would have no difficulty in running such hardening operations, there may be legacy clients whose limited computational power may limit their ability to run a large number of iterations (or whatever operations the hardening scheme requires).

Q18: Can any recommendations to avoid a user enumeration attack be given?
Yes. The OPAQUE draft (Section 5) discusses this issue and mitigation measures in quite detail.