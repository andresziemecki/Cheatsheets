# How to store secrets and keys

In `pubspect.yaml` we are going to add in the `dev_dependencies` the following:

``` yaml
dev_dependencies:
    flutter_config: ^1.0.5
```
control+s

Create in the root folder `.env`

```
API_URL=https://...
FABRIC_ID=pawan124
```

Then go to the main and make `main` async

``` dart

import 'package:flutter_config/flutter_config.dart';

void main async {
    WidgetsFlutterBindings.ensureInitialized(); # This ensure that everything was intialized correctly

    await FlutterConfig.LoadEnvironmentVariables();

    runApp(MyApp());

}

build... {
    print(FlutterConfig.get('API_URL'));
}

```


for android you have to do some changes, in `app/src/build.gradle`:

```
Below this following line:
apply from: "$flutterRoot/package...
Paste this:
apply from: project(':flutter_config').projectDir.getPath() + "/dotenv.gradle"
```

Maybe also you will add some dependencies on kotlin if you have some error with "invalid ID"



