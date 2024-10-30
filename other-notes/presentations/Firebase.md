# Introduction to Firebase

- Supongamos que tienes una muy buena idea para una aplicación y quieres empezar a construirla.

- Una arquitectura muy común comprende los siguientes elementos:
  * Una base de datos.
  * Un sistema de autenticación.
  * Un servidor de archivos multimedia.
  * Y un servidor que exponga una API a la aplicación cliente. []

- Ahora, supongamos que tu idea es muy buena y que mucha gente empieza a utilizar tu aplicación.

- Si bien esto es algo bueno, también significa que tendrás que pensar en cómo hacer que tu aplicación **escale**.
  - ¿Cómo haces para que tu API soporte miles de peticiones por minuto?
  - ¿Cómo haces que tu base de datos sea más rápida?
  - ¿Cómo te aseguras de que la autenticación sea completamente segura?
  - ¿Qué haces cuando los archivos multimedia empiezan a ocupar terabytes?
  - ¿Cómo migras tu aplicación a nuevas plataformas?

- Con todas estas dudas, uno se puede poner a pensar en si hay alguna forma fácil de hacer todo esto. Algo que me permita enfocarme más en la idea central y menos en la infraestructura. []

- Firebase es una plataforma de Google que trabaja bajo el modelo de Backend as a Service

- en el cual, tú ya no tienes que preocuparte por levantar un backend, programar una API, comunicarte con db, etcétera.

- con Firebase, tú solo debes enfocarte en el frontend de tu aplicación, no importa que tanto crezca []

- Firebase está construido sobre la infraestructura de Google Cloud, así que puedes estar seguro de que tu aplicación va a escalar sin problemas []

- Firebase ofrece soporte para múltiples plataformas cliente
  - incluyendo JavaScript, TypeScript para aplicaciones web
  - react, angular y vue si deseas usar un framework
  - IOS y swift para el ecosistema de apple
  - c++ y unity para desarrolladores de juegos
  - entre otras []

- respecto a *qué* módulos ofrece Firebase,
  - muchos de estos te servirán al empezar a construir tu aplicación
    - tenemos por un lado al módulo de autenticación
    - cloud firestore y realtime database para almacenar data no estructurada
    - cloud storage para almacenar archivos multimedia
    - y hosting para deployar tu aplicación web []
  - una vez que tu aplicación esté en producción
    - puedes usar crashlytics y performance monitoring para vigilar el rendimiento de tu aplicación
    - puedes usar test lab para probar tu aplicación en diferentes dispositivos []
  - y si deseas que tu aplicación crezca aún más
    - puedes usar in-app messaging y cloud messaging para enviar tanto pull como push notifications
    - a/b testing para probar cambios antes de lanzarlos a producción
    - y remote config para hacer cambios en la aplicación sin necesidad de que el usuario tenga que actualizarla []

- ahora, es posible que no todos estos módulos te sirvan []

	- la ventaja de Firebase es que tú puedes elegir qué servicios usar con tan solo unas cuántas líneas de código en la configuración de tu proyecto
