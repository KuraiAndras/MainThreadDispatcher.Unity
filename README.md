# MainThreadDispatcher.Unity

[![openupm](https://img.shields.io/npm/v/com.mainthreaddispatcher.unity?label=openupm&registry_uri=https://package.openupm.com)](https://openupm.com/packages/com.mainthreaddispatcher.unity/)

An implementation of the [IMainThreadDispatcher](https://github.com/KuraiAndras/MainThreadDispatcher) interface in Unity 3D

## Usage

Add a GameObject to you scene and add the UnityMainThreadDispatcher script to it. Make sure that this GameObject is in your scene.

```c#
//Getting an instance with static method
IMainThreadDispatcher dispatcher = UnityMainThreadDispatcherExtensions.Instance;

dispatcher.Invoke(() => Debug.Log("Hello 1"));
await dispatcher.InvokeAsync(() => Debug.Log("Hello 2"))

Button button = await dispatcher.InvokeAsync(() => GameObject.FindObjectOfType<Button>()))    
```

Calling the dispatcher is thread safe

## Gotchas

If you call UnityMainThreadDispatcherExtensions.Instance before the the GameObject containing it is instantiated you will get an exception.

If you call UnityMainThreadDispatcherExtensions.Instance for the first time from a thread other than the main unity thread, you will get an exception.

If there are multiple instances in you scene, then when calling UnityMainThreadDispatcherExtensions.Instance it will cache the first it finds. Preferably you only want one instance of it in your application, having multiple does not provide any performance benefit
