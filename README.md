This repository includes the source material for the CFRG PAKE selection process (summer of 2019), and a summary of the published reviews of the 8 candidates.



# PAKE Candidates

## Balanced Algorithms

| Name   | Submitters                  | Authoritative Source                                         | Additional Content                                           | Comments                                                     |
| ------ | --------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| SPAKE2 | Benjamin Kaduk, Watson Ladd | [draft-irtf-cfrg-spake2-09](https://tools.ietf.org/html/draft-irtf-cfrg-spake2-09) (updated) | [Requirements](Candidates/SPAKE2.md)                         |                                                              |
| J-PAKE | Feng Hao                    | [RFC8236](https://tools.ietf.org/html/rfc8236)               | [Requirements](Candidates/J-PAKE.pdf)                        |                                                              |
| SPEKE  | Dan Harkins                 | https://eprint.iacr.org/2014/585                             | [Requirements](Candidates/SPEKE.pdf)                         | Submitter note: The only thing to add is that when SPEKE is used with ECC a hash-to-curve method from the RFC that comes out of the CFRG (when it comes out of the CFRG) is necessary to produce the secret generator that SPEKE requires. |
| CPace  | Björn Haase                 | https://eprint.iacr.org/2018/286 (updated)                   | [Addendum](Candidates/CPace%20and%20AuCPace%20-%20addendum.pdf) <br> [Corrigendum](Candidates/CPace%20and%20AuCPace%20-%20corrigendum.pdf) <br> [Simulator Code](Candidates/simulatorCode_CPace_AuCPace_StrongAuCPace.ods)|                                                              |



## Augmented Algorithms

| Name    | Submitters    | Authoritative Source                                         | Additional Content                                           | Comments |
| ------- | ------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- |
| OPAQUE  | Hugo Krawczyk | [draft-krawczyk-cfrg-opaque-03](https://tools.ietf.org/html/draft-krawczyk-cfrg-opaque-03) | [Requirements](Candidates/OPAQUE.md)                         |          |
| AuCPace | Björn Haase   | https://eprint.iacr.org/2018/286 (updated)                   | [Addendum](Candidates/CPace%20and%20AuCPace%20-%20addendum.pdf) <br> [Corrigendum](Candidates/CPace%20and%20AuCPace%20-%20corrigendum.pdf) <br> [Simulator Code](Candidates/simulatorCode_CPace_AuCPace_StrongAuCPace.ods)|          |
| VTBPEKE | Guilin Wang   | https://www.di.ens.fr/david.pointcheval/Documents/Papers/2017_asiaccsB.pdf | [Requirements](Candidates/VTBPEKE.pdf)                       |          |
| BSPAKE  | Steve Thomas  |                                                              | [Information](Candidates/BSPAKE%20info.md) [Requirements](Candidates/BSPAKE.md) |          |



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



# Providing Feedback

To update the base material for a PAKE candidate or any of the reviews, please open an issue or, better yet, submit a pull request. Any substantial change should be reported to the [CFRG mailing list](https://mailarchive.ietf.org/arch/browse/cfrg/). Please include a link to the mailing list post.
