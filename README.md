# BitcoinZ Wallet

[Download here](https://github.com/bitcoinz-pod/bitcoinz-windows-wallet/releases)

Security Warnings
-----------------

**BitcoinZ is experimental and a work-in-progress.** Use at your own risk.

*BitcoinZ Desktop GUI Wallet is based on BitcoinZ Desktop GUI Wallet*
# [BitcoinZ](https://bitcoinz.global/) Desktop GUI Wallet

## Graphical user interface wrapper for the [BitcoinZ](https://bitcoinz.global/) command line tools

This program provides a Graphical User Interface (GUI) for the BitcoinZ client tools that acts as a wrapper and
presents the information in a user-friendly manner.

## Building, installing and running the Wallet GUI

Before installing the Desktop GUI Wallet you need to have BitcoinZ up and running. The following
[guide](https://github.com/bitcoinz-pod/bitcoinz-wallet/blob/master/README.md)
explains how to set up [BitcoinZ](https://bitcoinz.global/).

**For security reasons it is recommended to always build the GUI wallet program from GitHub**
**[source](https://github.com/bitcoinz-pod/bitcoinz-wallet/archive/master.zip).**
The details of how to build it are described below (easy to follow).


1. Operating system and tools

   As of October 2017 (BitcoinZ v1.0.9) this program is mostly tested on Linux and Windows.
   The Linux tools you need to build and run the Wallet GUI are Git, Java (JDK7 or later) and
   Ant. If using Ubuntu Linux, they may be installed via command:
   ```
   user@ubuntu:~/build-dir$ sudo apt-get install git default-jdk ant
   ```
   For RedHat/CentOS/Fedora-type Linux systems the command is (like):
   ```
   user@centos:~/build-dir$ sudo yum install java-1.8.0-openjdk git ant
   ```
   The name of the JDK package (`java-1.8.0-openjdk`) may vary depending on the Linux system, so you need to
   check it, if name `java-1.8.0-openjdk` is not accepted.
   If you have some other Linux distribution, please check your relevant documentation on installing Git,
   JDK and Ant. The commands `git`, `java`, `javac` and `ant` need to be startable from command line
   before proceeding with build.
   For MacOS use homebrew with the command like:
   ```
   machine:~/build-dir user$ brew install ant
   ```

2. Building from source code

   As a start you need to clone the bitcoinz-wallet Git repository:
   ```
   user@ubuntu:~/build-dir$ git clone https://github.com/bitcoinz-pod/bitcoinz-wallet.git
   ```
   Change the current directory:
   ```
   user@ubuntu:~/build-dir$ cd bitcoinz-wallet/
   ```
   Issue the build command:
   ```
   user@ubuntu:~/build-dir/bitcoinz-wallet$ ant -buildfile ./src/build/build.xml
   ```
   This takes a few seconds and when it finishes, it builds a JAR file `./build/jars/BitcoinZWallet.jar`.
   You need to make this file executable:
   ```
   user@ubuntu:~/build-dir/bitcoinz-wallet$ chmod u+x ./build/jars/BitcoinZWallet.jar
   ```
   At this point the build process is finished the built GUI wallet program is the JAR
   file `./build/jars/BitcoinZWallet.jar`

3. Installing the built BitcoinZ GUI wallet

   3.1. If you have built BitcoinZ from source code:

     Assuming you have already built from source code [BitcoinZ](https://bitcoinz.global/) in directory `/home/user/bitcoinz/src` (for example - this is the typical build dir. for BitcoinZ v1.0.9) which contains the command line tools `zen-cli` and `zend` you need to take the created file `./build/jars/BitcoinZWallet.jar` and copy it to directory `/home/user/bitcoinz/src` (the same dir. that contains `zen-cli` and `zend`). Example copy command:
      ```
      user@ubuntu:~/build-dir/bitcoinz-wallet$ cp ./build/jars/BitcoinZWallet.jar /home/user/bitcoinz/src    
      ```

4. Running the installed BitcoinZ GUI wallet

   It may be run from command line or started from another GUI tool (e.g. file manager).
   Assuming you have already installed [BitcoinZ](https://bitcoinz.global/) and the GUI Wallet `BitcoinZWallet.jar` in
   directory `/home/user/bitcoinz/src` one way to run it from command line is:
   ```
   user@ubuntu:~/build-dir/bitcoinz-wallet$ java -jar /home/user/bitcoinz/src/BitcoinZWallet.jar
   ```
   If you are using Ubuntu (or similar ;) Linux you may instead just use the file manager and
   right-click on the `BitcoinZWallet.jar` file and choose the option "Open with OpenJDK 8 Runtime".
   This will start the BitcoinZ GUI wallet.

   **Important:** the BitcoinZ configuration file `~/.zen/zen.conf` needs to be correctly set up for the GUI
   wallet to work. Specifically the RPC user and password need to be set in it like:
   ```
   rpcuser=username
   rpcpassword=wjQOHVDQFLwztWp1Ehs09q7gdjHAXjd4E

   ```


### License
This program is distributed under an [MIT License](https://github.com/bitcoinz-pod/bitcoinz-wallet/raw/master/LICENSE).

### Disclaimer

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

### Known issues and limitations

1. Limitation: if two users exchange text messages via the messaging UI TAB and one of them has a system clock, substantially running slow or fast by more than 1 minute, it is possible that this user will see text messages appearing out of order.
1. Limitation: if a messaging identity has been created (happens on first click on the messaging UI tab), then replacing the `wallet.dat` or changing the node configuration between mainnet and testnet will make the identity invalid. This will result in a wallet update error. To remove the error the directory `~/.ZENCashSwingWalletUI/messaging` may be manually renamed or deleted (when the wallet is stopped). **CAUTION: all messaging history will be lost in this case!**
1. Limitation: Wallet encryption has been temporarily disabled in BitcoinZ due to stability problems. A corresponding issue
[#1552](https://github.com/zcash/zcash/issues/1552) has been opened by the ZCash developers. Correspondingly
wallet encryption has been temporarily disabled in the BitcoinZ Desktop GUI Wallet.
1. Issue: GUI data tables (transactions/addresses etc.) allow copying of data via double click but also allow editing.
The latter needs to be disabled.
1. Limitation: The list of transactions does not show all outgoing ones (specifically outgoing Z address
transactions). A corresponding issue [#1438](https://github.com/zcash/zcash/issues/1438) has been opened
for the ZCash developers.
1. Limitation: The CPU percentage shown to be taken by zend on Linux is the average for the entire lifetime
of the process. This is not very useful. This will be improved in future versions.
1. Limitation: When using a natively compiled wallet version (e.g. `ZENCashSwingWalletUI.exe` for Windows) on a
very high resolution monitor with a specifically configured DPI scaling (enlargement) factor to make GUI
elements look larger, the GUI elements of the wallet actually do not scale as expected. To correct this on
Windows you need to right-click on `ZENCashSwingWalletUI.exe` and choose option:
```
Properties >> Compatibility >> Override High DPI scaling behavior >> Scaling Performed by (Application)
```
Example:

![DPI Scaling](https://github.com/bitcoinz-pod/bitcoinz-wallet/raw/master/docs/EXEScalingSettings.png "DPI Scaling")
