This repository includes the source material for the CFRG PAKE selection process (summer of 2019), and a summary of the published reviews of the 8 candidates.


# PAKE Candidates

## Balanced Algorithms

| Name   | Submitters                  | Round 2 | Authoritative Source                                         | Additional Content                                           | Comments                                                     |
| ------ | --------------------------- | ----- |------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| SPAKE2 | Benjamin Kaduk, Watson Ladd |&#10003;| [draft-irtf-cfrg-spake2-09](https://tools.ietf.org/html/draft-irtf-cfrg-spake2-09) (updated) | [Requirements](Candidates/SPAKE2.md)                         |                                                              |
| J-PAKE | Feng Hao                    || [RFC8236](https://tools.ietf.org/html/rfc8236)               | [Requirements](Candidates/J-PAKE.pdf)                        |                                                              |
| SPEKE  | Dan Harkins                 || https://eprint.iacr.org/2014/585                             | [Requirements](Candidates/SPEKE.pdf)                         | Submitter note: The only thing to add is that when SPEKE is used with ECC a hash-to-curve method from the RFC that comes out of the CFRG (when it comes out of the CFRG) is necessary to produce the secret generator that SPEKE requires. |
| CPace  | Björn Haase                 |&#10003;| https://eprint.iacr.org/2018/286 (updated)                   | [Addendum](Candidates/CPace%20and%20AuCPace%20-%20addendum.pdf) <br> [Corrigendum](Candidates/CPace%20and%20AuCPace%20-%20corrigendum.pdf) <br> [Simulator Code](Candidates/simulatorCode_CPace_AuCPace_StrongAuCPace.ods)|                                                              |



## Augmented Algorithms

| Name    | Submitters    | Round 2 | Authoritative Source                                         | Additional Content                                           | Comments |
| ------- | ------------- | ------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- |
| OPAQUE  | Hugo Krawczyk |&#10003;| [draft-krawczyk-cfrg-opaque-03](https://tools.ietf.org/html/draft-krawczyk-cfrg-opaque-03) | [Requirements](Candidates/OPAQUE.md)                         |          |
| AuCPace | Björn Haase   |&#10003;| https://eprint.iacr.org/2018/286 (updated)                   | [Addendum](Candidates/CPace%20and%20AuCPace%20-%20addendum.pdf) <br> [Corrigendum](Candidates/CPace%20and%20AuCPace%20-%20corrigendum.pdf) <br> [Simulator Code](Candidates/simulatorCode_CPace_AuCPace_StrongAuCPace.ods)|          |
| VTBPEKE | Guilin Wang   || https://www.di.ens.fr/david.pointcheval/Documents/Papers/2017_asiaccsB.pdf | [Requirements](Candidates/VTBPEKE.pdf)                       |          |
| BSPAKE  | Steve Thomas  ||                                                              | [Information](Candidates/BSPAKE%20info.md) [Requirements](Candidates/BSPAKE.md) |          |



# Summary of Reviews

The table below lists all reviews submitted to the CFRG mailing list. We mention only the first message of each mail thread. Reviewers who feel the initial does not reflect their latest position are requested to provide feedback (see below), preferably with a single message/file that covers their entire review.

| Author               | Algorithms Covered                  | Link                                                         |
| -------------------- | ----------------------------------- | ------------------------------------------------------------ |
| Scott Fluhrer        | All balanced                        | https://mailarchive.ietf.org/arch/msg/cfrg/HssFKRoUdM2kyVt4T9j_KPZqAmE <br> Re-review: https://mailarchive.ietf.org/arch/msg/cfrg/MZ-L7qSTDZEtC9hjhPNyGOhXUlQ |
| Bill Cox             | OPAQUE                              | https://mailarchive.ietf.org/arch/msg/cfrg/-B16hIOerRsHgoIxiln05TiJ17o |
| Valery Smyslov       | All candidates, for IKEv2           | https://tools.ietf.org/html/draft-smyslov-ikev2-pake-00      |
| Yoav Nir             | All candidates, for IKEv2           | https://mailarchive.ietf.org/arch/msg/cfrg/PWhIOQKBHapZ1Rpbd7Brr_JFIg8 |
| Kevin Lewi           | All augmented                       | https://mailarchive.ietf.org/arch/msg/cfrg/9E1owZANyjCEZW44IWj0u1Lze2I |
| Jonathan Hoyland     | All augmented, for TLS              | https://mailarchive.ietf.org/arch/msg/cfrg/FaY_3w5lWtygha0DTY5hJ9Yy7WU |
| Bjoern Tackmann      | All augmented (preliminary)         | https://mailarchive.ietf.org/arch/msg/cfrg/euWBn5Nku0WFGKQ6qcITaCKVM-k |
| Brian Warner         | All balanced, for Magic-Wormhole    | https://mailarchive.ietf.org/arch/msg/cfrg/BBQ2gwCECu5ouTJjE_CE6d9Rg-0 |
| Karthik Bhargavan    | All balanced, for TLS 1.3           | https://mailarchive.ietf.org/arch/msg/cfrg/5VhZLYGpzU8MWPlbMr2cf4Uc-nI |
| Steve Thomas         | All augmented                       | https://mailarchive.ietf.org/arch/msg/cfrg/AQtLrLSfATpOKxdjAakacnp2cBo |
| Thyla van der Merwe  | All candidates                      | https://docs.google.com/document/d/114t9rTk-d4nkTJZbEwwAn83uRy0ru2dm5qwOj0AMFaw/edit?usp=sharing |
| Stanislav Smyshlyaev | All balanced                        | https://docs.google.com/document/d/1czsluXWzGNnlzJDChcULAB_sqFaUWHzGMKjkjZDBMok/edit?usp=sharing |
| David Gotrik         | All candidates, for constrained IoT | [review](Reviews/dgotrik.pdf)                                |
| Tibor Jager          | All augmented                       | https://docs.google.com/document/d/1jAQm4lCUSJO73vyS14hF8Cl__grsOTF-Jj_CCStJDuU/edit?usp=sharing


# Overall Reviews by Crypto Review Panel

The table below lists all overall reviews submitted by the Crypto Review Panel members during Stage 5 of the PAKE selection process.

| Author               | Link                                                         |
| -------------------- | ------------------------------------------------------------ |
| Bjoern Tackmann      | https://mailarchive.ietf.org/arch/msg/cfrg/1sNu9USxo1lnFdzCL5msUFKBjzM |
| Stanislav Smyshlyaev | https://docs.google.com/document/d/1-vzeCtSrm7zfoolr1JQdNqtp6KrtVEjitkH0OmjKapc/edit?usp=sharing |
| Russ Housley         | https://docs.google.com/document/d/1L6lqueEB70C4QptEnjfWx-bhBdg6cT73ymmmm9WUAR0/edit?usp=sharing |
| Yaron Sheffer        | [review](https://tools.ietf.org/html/draft-sheffer-cfrg-pake-review-00)    |

# Questions for Round 2

1) (to SPAKE2): Can you propose a modification of SPAKE2 (preserving all existing good properties of PAKE2) with a correspondingly updated security proof, addressing the issue of a single discrete log relationship necessary for the security of all sessions (e.g., solution based on using M=hash2curve(A|B), N=hash2curve(B|A))?
2) (to CPace and AuCPace): Can you propose a modification of CPace and AuCPace (preserving all existing good properties of these PAKEs) with a correspondingly updated security proof (maybe, in some other security models), addressing the issue of requiring the establishment of a session identifier (sid) during each call of the protocol for the cost of one additional message?
3) (to all 4 remaining PAKEs) : Can the nominators/developers of the protocols please re-evaluate possible IPR conflicts between their candidates protocols and own and foreign patents? Specifically, can you discuss the impact of U.S. Patent 7,047,408 (expected expiration 10th of march 2023) on free use of SPAKE2 and the impact of EP1847062B1 (HMQV, expected expiration October 2026) on the free use of the RFC-drafts for OPAQUE?
4) (to all 4 remaining PAKEs) What can be said about the property of "quantum annoyance" (an attacker with a quantum computer needs to solve [one or more] DLP per password guess) of the PAKE?
5) (to all 4 remaining PAKEs) What can be said about "post-quantum preparedness" of the PAKE?

# Answers on Round 2

| Protocol               | Link                                                         |
| -------------------- | ------------------------------------------------------------ |
| CPace and AuCPace      | https://mailarchive.ietf.org/arch/msg/cfrg/eRNe0SYH3lwHifwZkmqHRy4pdNE |
| SPAKE2 | https://mailarchive.ietf.org/arch/msg/cfrg/senXefqczpUZo26B35ekz8d3iLo |
| OPAQUE         | https://mailarchive.ietf.org/arch/msg/cfrg/EJnaKEh_RamzghcjAik5v9_Fwf8 |

Related information on IPR (SPAKE2): https://datatracker.ietf.org/ipr/4018/

# Reviews by Crypto Review Panel, Round 2

The table below lists all overall reviews submitted by the Crypto Review Panel members during Stage 5 of the PAKE selection process.

| Author               | Link                                                         |
| -------------------- | ------------------------------------------------------------ |
| Bjoern Tackmann      | https://mailarchive.ietf.org/arch/msg/cfrg/eo8O6JYPmWY6L9TlcIXStFy5gNQ/ |
| Julia Hesse          | https://mailarchive.ietf.org/arch/msg/cfrg/47pnOSsrVS8uozXbAuM-alEk0-s/ |
| Russ Housley         | https://mailarchive.ietf.org/arch/msg/crypto-panel/r3ktVcmPA-POVMNjVBmY84lTOHA/ |
| Scott Fluhrer        | https://mailarchive.ietf.org/arch/msg/cfrg/JwBPf_71G6JcfUttFw9MbvnIDCU/   |

# Providing Feedback

To update the base material for a PAKE candidate or any of the reviews, please open an issue or, better yet, submit a pull request. Any substantial change should be reported to the [CFRG mailing list](https://mailarchive.ietf.org/arch/browse/cfrg/). Please include a link to the mailing list post.

