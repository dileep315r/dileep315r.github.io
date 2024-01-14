1. The setContent block defines the activity's layout where composable functions are called.
2. Composable functions can only be called from other composable functions.
3. Jetpack Compose uses a Kotlin compiler plugin to transform these composable functions into the app's UI elements.
4. To make a function composable, add the @Composable annotation.
5. UI elements are hierarchical, with elements contained in other elements. In Compose, you build a UI hierarchy by calling composable functions from other composable functions.
6. The Column function lets you arrange elements vertically. Add Column to the MessageCard function.
You can use Row to arrange items horizontally and Box to stack elements.
7. Enrich your message card by adding a profile picture of the sender. Use the Resource Manager to import an image from your photo library or use this one. Add a Row composable to have a well structured design and an Image composable inside it.
8. Your message layout has the right structure but its elements aren't well spaced and the image is too big! To decorate or configure a composable, Compose uses modifiers. They allow you to change the composable's size, layout, appearance or add high-level interactions, such as making an element clickable. You can chain them to create richer composables. You'll use some of them to improve the layout.
9. Jetpack Compose provides an implementation of Material Design 3 and its UI elements out of the box. You'll improve the appearance of our MessageCard composable using Material Design styling.
10. Material Design is built around three pillars: Color, Typography, and Shape. You will add them one by one
11. With Shapeyou can add the final touches. First, wrap the message body text around a Surface composable. Doing so allows customizing the message body's shape and elevation. Padding is also added to the message for a better layout.
12. Dark theme (or night mode) can be enabled to avoid a bright display especially at night, or simply to save the device battery. Thanks to the Material Design support, Jetpack Compose can handle the dark theme by default. Having used Material Design colors, text and backgrounds will automatically adapt to the dark background.
13. You can create multiple previews in your file as separate functions, or add multiple annotations to the same function.
14. Color choices for the light and dark themes are defined in the IDE-generated Theme.kt file
15. For this use case, use Compose’s LazyColumn and LazyRow. These composables render only the elements that are visible on screen, so they are designed to be very efficient for long lists.
16. To store this local UI state, you need to keep track of whether a message has been expanded or not. To keep track of this state change, you have to use the functions remember and mutableStateOf.
17. Composable functions can store local state in memory by using remember, and track changes to the value passed to mutableStateOf
18. Composables (and their children) using this state will get redrawn automatically when the value is updated. This is called recomposition.
19. 
