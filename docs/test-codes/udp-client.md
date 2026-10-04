```haxe
// /scripts/TestModule.hxc
import funkin.modding.events.ScriptEvent;
import funkin.modding.module.ModuleHandler;
import funkin.modding.module.Module;

class TestModule extends Module {
    public function new() {
        super("test");
    }

    override function onCreate(event:ScriptEvent) {
        var suilUDPSocketManager:Null<SuilUDPSocketManager> = ModuleHandler.getModule("suil-udp-socket-manager");
        if(suilUDPSocketManager == null) {
            return;
        }

        var id = "test";

        suilUDPSocketManager.createSocket(id);
        suilUDPSocketManager.bindSocket(id, 5340);

        suilUDPSocketManager.addEventListener(id, suilUDPSocketManager.DATA, (event) -> {
            trace(event.data);
        });

        suilUDPSocketManager.send(id, "testtesttest", "127.0.0.1", 1234);
    }

    var updateCount = 0.0;
    var received = false;
    override function onUpdate(event:UpdateScriptEvent) {
        if(updateCount > 2 && !received) {
            var suilUDPSocketManager:Null<SuilUDPSocketManager> = ModuleHandler.getModule("suil-udp-socket-manager");
            if(suilUDPSocketManager == null) {
                return;
            }

            suilUDPSocketManager.receive("test");
            received = true;
        }
        else { // i know received what bruh
            updateCount += event.elapsed;
        }
    }
}
```
