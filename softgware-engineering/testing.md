#### Test pyramid
1. The pyramid is based on the assumption that the earlier you catch a bug the better — which is largely right
2. and that higher-level tests are slower to write/run and costlier to maintain.
3. What I feel is missing though, is that as you move up you also get more stable contracts, and a higher chance of changing implementation under the hood. This makes integration tests very valuable, while unit tests… a bit less so.
4. No pyramid, no trophy -- write tests for high ROI
   1. Should facilitate rapid release to production with confidence of not breaking production.
   2. Protect against refactorings.
#### Test driven development (TDD)
https://www.ibm.com/garage/method/practices/code/practice_test_driven_development/
Three basic laws proposed by Uncle Bob which state that code should be written to make test cases pass, write only just enough test cases, write just enough code for the test cases to pass.
Advantages
1. It makes your code flexible and extensible. The code can be refactored or moved with minimal risk of breaking code.
2. It can enable faster innovation and continuous delivery because the code is robust.
Testimonial from IBM. There may be inherent bias in the experiment.
3. At IBM, teams found that the built-in unit testing produces better code. One team recently worked on a project where a small portion of the team used TDD while the rest wrote unit tests after the code. When the code was complete, the developers that wrote unit tests were surprised to see that the TDD coders were done and had more solid code.

