# Working with jCrystal on the frontend

jCrystal is a full-stack framework that aims to reduce code rewrites, moreover, on your frontend clients it will help you:

- Access your web services with zero effort.
- Access your data model with zero effort.

This will be possible thanks to the code that jCrystal generates using the **descriptions of the web services and entities of the backend**. As such, please take into account that to use jCrystal on your frontend you **must** have a backend in jCrystal that has and uses frontend clients. If you already have a backend, please read [this guide to learn how to add clients to your backend](../clients/general.md).


jCrystal generates utility code usually in one folder and one or more sets of files depending on the frontend platform.  As a frontend developer, this means that:

- You are in charge of creating your frontend project.

    jCrystal will make everything easier for you, but you are still in charge of creating your frontend project. Don't worry, that only means you can customize it as much as you want!

    That also means jCrystal can be used on a frontend project that's already created.

- You **can use your own code editor for your frontend client**.

    Feel free to use the code editor that you are most familiar with on your client-side. jCrystal is here to make you **faster**, not to force you to change everything you know about frontend development

- You are in charge of setting up the project to support jCrystal.

    Don't worry, this usually means adding a couple of dependencies to your frontend project. :wink:

## What's next
Setup your frontend app to use jCrystal:
- [Angular](../frontend/angular/setup.md).
- [Android](../frontend/android/setup.md).
- [iOS](../frontend/iOS/setup.md).