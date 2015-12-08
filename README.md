## 1、导入CoreTelephony.framework
## 2、引入两个头文件
### import <CoreTelephony/CTCallCenter.h>
### import <CoreTelephony/CTCall.h>
## //3、定义变量(警告，最好不要在viewDidLoad中定义局部变量，最好是这种全局变量，否则因为变量被释放等无法接收来电话等的消息)
##@property(strong,nonatomic) CTCallCenter *callCenter;
##4、创建并接收回调等
```
	_callCenter = [[CTCallCenter alloc] init];
 
    _callCenter.callEventHandler = ^(CTCall* call) {
        if ([call.callState isEqualToString:CTCallStateDisconnected])
        {
            NSLog(@"挂断了电话咯 Call has been disconnected");
            
        }
        else if ([call.callState isEqualToString:CTCallStateConnected])
        {
            NSLog(@"电话通了 Call has just been connected");
        }
        else if([call.callState isEqualToString:CTCallStateIncoming])
        {
            NSLog(@"来电话了 Call is incoming");
            // 用来做暂停录音之类的。
        }
        else if ([call.callState isEqualToString:CTCallStateDialing])
        {
            NSLog(@" 正在播出电话 call is dialing");
        }
        else
        {
            NSLog(@"嘛都没做 Nothing is done");
        }
    };
```

--------
## 备注，接电话打印的流程：
     1.Call is incoming
     2. Call has just been connected
     3.Call has been disconnected
## 打电话的流程：
     1.call is dialing
     2.Call has just been connected
     3.Call has been disconnected
   
####  这个播出电话的测试我在其他项目测试过，不过这里到后台好像就被挂起了，因为也没什么定位之类的让他多存留一会，然后我在app delegate中的applicationDidEnterBackground里加了一段代码，保证了能测试出来。
