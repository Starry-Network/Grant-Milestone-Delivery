# Evaluation

- **Status:** Accepted
- **PR Link:** Spartan POC Consensus Module: [Accepted W3F Grant App PR](https://github.com/w3f/Open-Grants-Program/pull/357).
- **Milestone:** 1
- **Kusama Identity:** GqVuCLydpKFFx9w3CbBF1nD8xWxtA1UM5npCZxPVoZq7CjQ
- **Previously successfully merged evaluation:** None

| Number | Deliverable            | Accepted              | Link                                                                                                                                                    | Evaluation Notes                                                                                                                                         |
| ------ | ---------------------- | --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0a.    | License                | <ul><li>[X]</li></ul> | -                                                                                                                                                       | Placed in each module: Apache 2.0, Unlicense and GPL-3.0-or-later WITH Classpath-exception-2.0                                                           |
| 0b.    | Documentation          | <ul><li>[X]</li></ul> | [Node Template Spartan Readme](https://github.com/subspace/substrate/blob/b9a561c0760e638110b725e2509632e9089f7d43/bin/node-template-spartan/README.md) | Requested adjustments have all been incorporated                                                                                                         |
| 0c.    | Testing Guide          | <ul><li>[X]</li></ul> | [From Readme](https://github.com/subspace/substrate/blob/b9a561c0760e638110b725e2509632e9089f7d43/bin/node-template-spartan/README.md#run-tests)        | Clear instructions on how to build/run/test the deliveries, all modules have a minimal set of unit tests (where applicable at current development stage) |
| 0d.    | Article                | <ul><li>[X]</li></ul> | [Article](https://medium.com/@jeremiahwagstaff/bringing-poc-consensus-to-substrate-d49d49a912bd)                                                        |                                                                                                                                                          |
| 1.     | Design Document        | <ul><li>[X]</li></ul> | [From `pallet_spartan`](https://github.com/subspace/substrate/blob/a88f2703ee153cdb5ae67e6e047bc86076370b60/frame/spartan/design.md)                    |                                                                                                                                                          |
| 2.     | `sp_consensus_PoC`     | <ul><li>[X]</li></ul> | [Module Link](https://github.com/subspace/substrate/tree/bfe9476526780ba4182d518764bc11e320222cc5/primitives/consensus/poc)                             |                                                                                                                                                          |
| 3.     | `sc_consensus_PoC`     | <ul><li>[X]</li></ul> | [Module Link](https://github.com/subspace/substrate/tree/a48694d8a31afb369bdaa57d34a80e52f8c8445b/client/consensus/poc)                                 | Team reasonably argued why previously requested adjustments regarding tests can be postponed to upcoming milestone deliveries                            |
| 4.     | `sp_consensus_spartan` | <ul><li>[X]</li></ul> | [Module Link](https://github.com/subspace/substrate/tree/385ba07f119f7b5163cb4876771a5854a24028e9/primitives/consensus/spartan)                         |                                                                                                                                                          |
| 5.     | `sc_consensus_spartan` | <ul><li>[X]</li></ul> | None                                                                                                                                                    | This is essentially the functionality provided by `spartan-farmer` and proved unessecary.                                                                |
| 6.     | `pallet_spartan`       | <ul><li>[X]</li></ul> | [Module Link](https://github.com/subspace/substrate/tree/c0e058ff8da7a8ba25dde936adc9eecb4d22beb0/frame/spartan)                                        |                                                                                                                                                          |
| 7.     | `spartan_farmer`       | <ul><li>[X]</li></ul> | [Module Link](https://github.com/subspace/spartan-farmer/tree/b6d85cac27b8124a500c0b801bb2441b76db8542)                                                 | All requested adjustments incorporated                                                                                                                   |
| 8.     | `spartan_client`       | <ul><li>[X]</li></ul> | [Module Link](https://github.com/subspace/substrate/tree/b9a561c0760e638110b725e2509632e9089f7d43/bin/node-template-spartan)                            | All requested adjustments either incorporated or reasonably argued.                                                                                      |
| 9.     | Docker                 | <ul><li>[X]</li></ul> | [From Readme](https://github.com/subspace/substrate/blob/b9a561c0760e638110b725e2509632e9089f7d43/bin/node-template-spartan/README.md#run-with-docker)  |                                                                                                                                                          |

Ideally all links inside the above table should include the commit hash,
which was used for testing the delivery. It should also be checked if the software is published under the correct open-source license.

## General Notes

IMHO the team delivered on their promises and shipped an overall solid M1 which I suggest for approval as all of the remarks [discussed here](https://github.com/w3f/Grant-Milestone-Delivery/pull/165#issuecomment-835794353) have been addressed.

Besides some minor caveats the documentation is very comprehensive, well-structured and understandable so that the process to get the deliveries up and running was straight forward. Besides the instructions on how to build and run things, both the design paper and the blog post are clear, well written and helped to understand their solution, vision and roadmap better.

Although this is just the first milestone and it's of course early days, the spartan-farmer could be improved a bit in terms of ease-of-use to make it more resilient outside of the happy case. For example the spartan-farmer wasn't very verbose at telling the user to erase previously created plots when attempting to create another plot later on or the sensitivity to connection interruptions when farming, which could be a bit daunting during development (when you restart/rebuild your node couple of times) and of course in production. **Update**: Both issues have been acknowledged and partly addressed with subsequent updates during the review process.

For the primitives, crates and pallets within substrate (deliveries 2-6 & 8), the team was able to start off based on existing implementations (BABE, VRF, ...) and adapt them to their needs - therefore it's clear that they were able to follow good practices quite easily and its great to see that they consider/extend existing solutions rather than re-inventing the wheel – however with the spartan-farmer they had to write and structure the code mostly on their own. This might have led to less inline documentation, minimal testing and may have left some potential to better structure the code – but this is just a first and high-level impression as I'm not experienced with Rust and a second opinion on this would be helpful. Again, overall the farmer does what it should and delivers as expected. **Update**: The team has improved inline documentation with updates during the review process.

Regarding licensing, I have to mention that besides `Apache-2.0` and `Unlicense`, they are also using the `GPL-3.0-or-later WITH Classpath-exception-2.0` license within [sc_consensus_poc](https://github.com/subspace/substrate/blob/poc/client/consensus/poc/README.md), which hasn't been mentioned in the [Guidelines](https://github.com/w3f/General-Grants-Program/blob/master/grants/milestone-deliverables-guidelines.md) specifically.

Automated testing could always be a bit more, as it seems minimal for the farmer and they've limited tests to the adaptation of pre-existing ones within substrate (where applicable within milestone 1). But there was at least a minimum set of tests in each delivery, and they have thought of testing from the beginning and plan to extend their automated tests with subsequent milestones. Should be fine for the approval of this milestone.

The team was quick to respond to requested adjustments during the review process and either resolved issues right away or were able to reasonably argue why they would prefer to not incorporate some of the remarks or postpone them to later milestones. Communication was respectful and friendly at all times.