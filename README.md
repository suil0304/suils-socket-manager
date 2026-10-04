# suils-socket-manager
A V-Slice library (mod) about socket management or something
-------------------------------------

<div style="display: flex; flex-direction: row; justify-content: center; width: 100vm;">
	<image src="./_polymod_icon.png" style="width: 200px" />
</div>
<ol style="display: flex; flex-direction: row; justify-content: center; width: 100vm; list-style-type: none;">
	<li>
		<a href="https://gamebanana.com/tools/24310">
			<div style="font-size: 0.75em; box-sizing: border-box; padding: 6px 8px; border-radius: 8px; background-color: rgb(255, 245, 112);">GameBanana</div>
		</a>
	</li>
</ol>

# Overview
A V-Slice's Power?ful Socket Management Library.

please check api document [here](./docs/API.md)

# Feature
## TCP
completed

- \+ Manager
	- \+ Auto Destroy on Module Destroyed
- \+ Event Programming (WIP (maybe))
- \+ Custom Contract (Header Schema and ETC)
- \+ Connect Timeout (No connect handshake received)
- \+ Refresh Timeout (On client received data)

## UDP
*depend on V-Slice 0.9 Preview (OpenFL 0.9.5)*

wip (openfl issue (maybe))

- \+ Manager
- \+ Event Programming (WIP)
	- \+ Auto Destroy on Module Destroyed
- \- No connect method
- \- Wrong receive

## Custom Contract
TCP only (2026-10-05)

***TCP***
- Header Schema
- Connect Handshake
- Close Handshake
- Connect Timeout
- Refresh Timeout

## Development
### Requirements
- Haxe
- Visual Studio Code
- Friday Night Funkin' 0.9 Preview 3

### Setup
```bash
git clone https://github.com/suil0304/suils-socket-manager.git
```

Install required VScode extensions.

Set up Funkin IDE settings.
1. Run `>Funkin FCPKG: Setup haxelib` (VScode Command Palette)
2. Select `Official FNF (V-Slice) Ver. 0.9.0-prev3`

Run FNF from Command Prompt.

### TCP
#### Test Codes
***Funkin' Client Script***
[TCP Client Code](./docs/test-codes/tcp-client.md)

***Server Code***
[TCP Server Code](./docs/test-codes/tcp-server.md)

#### Expected Output
***FNF***
```
connected
echo thing
echo thing
echo thing
echo thing
echo thing
```

***Server***
```
Listening on 127.0.0.1:8080
Client connected
Received: echo thing
Received: echo thing
Received: echo thing
Received: echo thing
Received: echo thing
```

### UDP
#### Test Codes
***Funkin' Client Script***
[UDP Client Code](./docs/test-codes/udp-client.md)

***Server Code***
[UDP Server Code](./docs/test-codes/udp-server.md)

#### Expected Output
***FNF***
```
testtesttest
```

***Server***
```
Received: testtesttest
```

