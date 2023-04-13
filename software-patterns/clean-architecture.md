#### Follow the principles in [this uncle bob talk](https://www.youtube.com/watch?v=asLUTiJJqdE) to structure the code.
![img](https://stackoverflow.com/questions/58239166/i-can-not-understand-clean-architectures-part-mvp-from-uncle-bob-book)
1. A good architecture revelas intent of the software. For example, just by looking at the folder structure we are able to describe what the software does. Usecase focused than tool focused. Package by feature than package by level.
2. Architecture is about intent.
3. Good architectures create structures that allow decisions to be deferred. For example, delay the decision of the database to use, delay the decision of the external service to use.
4. Usecase object takes in a data structure and emits another data structure.
5. Entities, interactors(usecase logic), UI & delivery mechanism(Web, desktop app etc..). Interface as boundaries between them. Entity belongs to enterprise, they are application independent. Interactor belongs to application. Enterprise may have multiple applications.
6. Database hanging off the side, just like an appendix.
7. Presenter constructs view model from a interactor output object.
8. View constructs view from view model. Dumb, no logic, just substitutes values.
9. Controller takes the data, constructs objects for interactors, orchestrates among interactors.
10. View is not coupled with business/interactor/usecase objects.
11. Keep the frameworks out of your application. Frameworks are secondary. Application is primary.
12. Keep frameworks at arms length.
13. View Model doesn't know about the device and rendering.

