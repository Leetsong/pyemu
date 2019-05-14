pyemu
=====

Enables android emulator in your python script.

### Purpose

This python package is a wrapper for standard android emulator (via telnet) implementation. It allows you to execute android emulator commands in your python script.

### What's supported?

Currently following adb commands are **supported**:
* auth
* avd

### What's not supported?

Currently following adb commands are **not supported**:

* fold
* unfold
* kill
* ping
* rotate
* crash
* crash-on-exit
* debug
* redir
* geo
* event
* power
* gsm
* cdma
* sensor
* sms
* finger

### What's TODO?

* Add `with` context manager
* Add adapters to provide more easy-to-use functions (see [here](http://gogs.njuics.cn/android/anip/src/master/src/anip/emu.py)), e.g.
    * save/load snapshot (e.g., sdk version)
    * ...

### How to install?

Download with help of git:

```
$ git clone https://github.com/Leetsong/pyemu.git
```

### How to use?

Put dir pyemu to your own project, a demo example shows here.

``` python
emu = AndroidEmu(log_output=False, log_command=True)
emu.open(host='localhost', port=5554)

try:
    retc, result = emu.auth(Path.home() / '.emulator_console_auth_token')
    print('>> [{}]\n{}\n'.format(retc, result))

    retc, result = emu.avd('snapshot', 'list')
    print('>> [{}]\n{}\n'.format(retc, result))

    retc, result = emu.network('delay', AndroidEmuNetworkDelay.customize(1000, 2000))
    print('>> [{}]\n{}\n'.format(retc, result))
except Exception as e:
    print(e)
finally:
    emu.close()
```

### How to contribute?

* Implement emulator commands which are currently not supported by the module (see above)
* Bring your own ideas!
