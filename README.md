This repository includes the source material for the CFRG PAKE selection process (summer of 2019), and a summary of the published reviews of the 8 candidates.



# PAKE Candidates

## Balanced Algorithms

| Name   | Submitters                  | Authoritative Source                                         | Additional Content                                           | Comments                                                     |
| ------ | --------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| SPAKE2 | Benjamin Kaduk, Watson Ladd | [draft-irtf-cfrg-spake2-08](https://tools.ietf.org/html/draft-irtf-cfrg-spake2-08) | [Requirements](Candidates/SPAKE2.md)                         |                                                              |
| J-PAKE | Feng Hao                    | [RFC8236](https://tools.ietf.org/html/rfc8236)               | [Requirements](Candidates/J-PAKE.pdf)                        |                                                              |
| SPEKE  | Dan Harkins                 | https://eprint.iacr.org/2014/585                             | [Requirements](Candidates/SPEKE.pdf)                         | Submitter note: The only thing to add is that when SPEKE is used with ECC a hash-to-curve method from the RFC that comes out of the CFRG (when it comes out of the CFRG) is necessary to produce the secret generator that SPEKE requires. |
| CPace  | Björn Haase                 |                                                              | [Updated Paper](Candidates/CPace%20and%20AuCPace%20Updated.pdf) [Addendum](Candidates/CPace%20and%20AuCPace%20-%20addendum.pdf) [Corrigendum](Candidates/CPace%20and%20AuCPace%20-%20corrigendum.pdf) |                                                              |



## Augmented Algorithms

| Name    | Submitters    | Authoritative Source                                         | Additional Content                                           | Comments |
| ------- | ------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- |
| OPAQUE  | Hugo Krawczyk | [draft-krawczyk-cfrg-opaque-02](https://tools.ietf.org/html/draft-krawczyk-cfrg-opaque-02) | [Requirements](Candidates/OPAQUE.md)                         |          |
| AuCPace | Björn Haase   |                                                              | [Updated Paper](Candidates/CPace%20and%20AuCPace%20Updated.pdf) [Addendum](Candidates/CPace%20and%20AuCPace%20-%20addendum.pdf) [Corrigendum](Candidates/CPace%20and%20AuCPace%20-%20corrigendum.pdf) |          |
| VTBPEKE | Guilin Wang   | https://www.di.ens.fr/david.pointcheval/Documents/Papers/2017_asiaccsB.pdf | [Requirements](Candidates/VTBPEKE.pdf)                       |          |
| BSPAKE  | Steve Thomas  |                                                              | [Information](Candidates/BSPAKE%20info.md) [Requirements](Candidates/BSPAKE.md) |          |



# Summary of Reviews

The table below summarizes all reviews submitted to the CFRG mailing list. We quote only the first message of each mail thread. Reviewers who feel the summary does not reflect their latest position are requested to provide feedback (see below).

# Providing Feedback

To update the base material for a PAKE candidate or any of the reviews, please open an issue or, better yet, submit a pull request. Any substantial change should be reported to the [CFRG mailing list](https://mailarchive.ietf.org/arch/browse/cfrg/). Please include a link to the mailing list post.
