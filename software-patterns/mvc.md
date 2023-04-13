### [MVC patterns](https://blog.bytebytego.com/p/ep49-api-architectural-styles)
![Architectural patterns](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F61af5cdf-2a56-4ae8-ad09-eb703c26989d_1280x1755.jpeg)
1. Controller," "presenter," and "view-model" are translators that mediate between the view and the model ("entity" in the VIPER pattern). The patterns are confusing since they represent almost same concepts, slightly modified versions are being used in different contexts.
2. MVC
   ![img](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller#/media/File:MVC-Process.svg)
   1. This is done to separate internal representations of information from the ways information is presented to and accepted from the user.
   2. I see slight variations when people implemented it.
   3. The decoupling of the components is the essence of the technique.
3. MVP
   ![img](https://upload.wikimedia.org/wikipedia/commons/d/dc/Model_View_Presenter_GUI_Design_Pattern.png)
   1. MVP is a user interface architectural pattern engineered to facilitate automated unit testing and improve the separation of concerns in presentation logic
   2. The model is an interface defining the data to be displayed or otherwise acted upon in the user interface.
   3. The view is a passive interface that displays data (the model) and routes user commands (events) to the presenter to act upon that data.
   4. The presenter acts upon the model and the view. It retrieves data from repositories (the model), and formats it for display in the view.
   5. user input --> view --> presenter --> model --> presenter --> view --> user sees updated screen
4. Model view view model
   ![img](https://upload.wikimedia.org/wikipedia/commons/8/87/MVVMPattern.png)
5. MVVM-c
6. VIPER
   ![img](https://koenig-media.raywenderlich.com/uploads/2020/02/viper.png)
   1. Clean code architecture
   2. This is what I have been using throughout the career.
   3. This separation is borne out of “Uncle” Bob Martin’s Clean Architecture paradigm.
