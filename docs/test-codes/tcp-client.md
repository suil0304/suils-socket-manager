```haxe
// /scripts/TestModule.hxc
import funkin.modding.events.ScriptEvent;
import funkin.modding.module.ModuleHandler;
import funkin.modding.module.Module;

class TestModule extends Module {
    override function onCreate(event:ScriptEvent) {
        var suilSocketManager:Null<SuilSocketManager> = ModuleHandler.getModule("suil-socket-manager");
        if(suilSocketManager == null) {
            return;
        }

        var suilContractManager:Null<SuilContractManager> = ModuleHandler.getModule("suil-contract-manager");
        if(suilContractManager == null) {
            return;
        }

        var id = "test";

        suilSocketManager.createSocket(id, suilContractManager.getTCPContractDefault());

        suilSocketManager.addEventListener(id, suilSocketManager.CONNECT, (eventData) -> {
            trace("connected");
            trace(eventData.remoteAddress);
            trace(eventData.remotePort);

            suilSocketManager.sendBytes(
                id,
                [
                    "payloadSize" => 10
                ],
                "echo thing"
            );
            suilSocketManager.sendBytes(
                id,
                [
                    "payloadSize" => 10
                ],
                "echo thing"
            );
            suilSocketManager.sendBytes(
                id,
                [
                    "payloadSize" => 10
                ],
                "echo thing"
            );
            suilSocketManager.sendBytes(
                id,
                [
                    "payloadSize" => 10
                ],
                "echo thing"
            );
            suilSocketManager.sendBytes(
                id,
                [
                    "payloadSize" => 10
                ],
                "echo thing"
            );
        });

        suilSocketManager.addEventListener(id, suilSocketManager.DATA, (eventData) -> {
            trace(eventData.payloadString);
        });

        suilSocketManager.connectSocket(id, "127.0.0.1", 8080);
    }

    override function onDestroy(event:ScriptEvent) {
        var suilSocketManager:Null<SuilSocketManager> = ModuleHandler.getModule("suil-socket-manager");
        if(suilSocketManager == null) {
            return;
        }

        suilSocketManager.destroySocket("test");
    }
}
```
