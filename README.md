# Android Service with MethodChannel

### Service Class
<p></p>

```java
@Override
public void onCreate() {
    super.onCreate();
    Toast.makeText(this, "Start Service", Toast.LENGTH_SHORT).show();
}

@Override
public void onDestroy() {
    super.onDestroy();
    Toast.makeText(this, "Stop Service", Toast.LENGTH_SHORT).show();
}
```
### MainActivity Class

```java
@Override
public void configureFlutterEngine(@NonNull FlutterEngine flutterEngine) {
    super.configureFlutterEngine(flutterEngine);
    new MethodChannel(flutterEngine.getDartExecutor().getBinaryMessenger(),CHANNEL)
            .setMethodCallHandler(
                    (call,result)->{
                        if(call.method.equals("service")){
                            startService(new Intent(MainActivity.this,MyService.class));
                        }
                        result.success(message);
                        /// resuts succes must be returned list
                    }
            );
}
```

### Dart

```dart
/// same name with android mainactivity class method name
static const platform = MethodChannel('sample.flutter.dev/service');
platform.invokeListMethod('service');

```