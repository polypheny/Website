---
layout: plain
title: UI Development Environment
description: >
  How to setup-up a Polypheny-UI development environment.
hide_description: true
---

This guideline describes how to setup-up a development environment for the [Polypheny-UI](https://github.com/polypheny/Polypheny-UI). In the following, we describe two approaches.

First, make sure you have [node.js](https://nodejs.org/en/) installed. Then, clone [Polypheny-UI](https://github.com/polypheny/Polypheny-UI), open the root folder and run

```
npm install
```

If you haven't installed Angular yet, do so by executing

```
npm install -g @angular/cli
```

Now you can run
```
ng serve --aot -o
```

You should now be able to open the UI in your browser by entering the url [http://localhost:4200/](http://localhost:4200/). Please make sure you have a running instance of Polypheny-DB.



## Using gradle
If you want to build the project without having to install NodeJS and Angular, you can do so by executing

```
./gradlew npm_install
```

The Angular Live Development Server can be started using

```
./gradlew npm_start
```

You should now be able to open the UI in your browser by entering the url [http://localhost:4200/](http://localhost:4200/). Please make sure you have a running instance of Polypheny-DB.