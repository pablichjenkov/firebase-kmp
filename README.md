This repo host a Swift Package with the implementation of the abstract KMP module located at:
https://github.com/pablichjenkov/macao-marketplace/blob/dev/auth-firebase/src/iosMain/kotlin/com/macaosoftware/plugin/account/FirebaseAuthKmpWrapper.kt
<br/>
This package is a wrapper of the Firebase Authorization swift API defined in above link.
<br/>
<br/>
Kotlin can't talk to swift directly but can consume a Kotlin interface which implementation is made with swift. This project is a proof of concept on how to host an SPM package in a different repo than composeApp. To consume this package from a KMP project, there are some requirements to be met:
<br/>
1. The KMP project umbrella module has to produce a framework named **ComposeApp**.

    As of now, by convention, KMP should only export 1 framework to the iOS integration App, so we agree on the swift module to **import ComposeApp** as the provider of the KMP interfaces.

2. The KMP abstraction module has to be included in gradle using **api**(...) and **not** using **implementation**(...).

    This is because we have to export that module and only dependencies consumed as **api**(...) can be exported to the umbrella module.

That is all you need.
