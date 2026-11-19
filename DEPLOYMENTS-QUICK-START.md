<a id="cli-install"></a>

# Install Confluent CLI

Install the Confluent CLI on macOS, Linux, or Windows using Homebrew, APT,
YUM, Docker, or a direct binary download. This topic also includes
[other installation methods](#other-cli-install-methods).

Before you install, verify that your system [meets the prerequisites](overview.md#cli-requirements).

### Homebrew

macOS and Linux users can install the latest version of Confluent CLI using
the following [Homebrew](https://brew.sh/) command:

```text
brew install confluentinc/tap/cli
```

### APT

If you are a Debian or Ubuntu user, you can install the latest version of
Confluent CLI using the APT package manager:

1. Install `curl` and `gpg` (if you have not already installed them).
   ```shell
   sudo apt install curl gnupg
   ```
2. Install the Confluent CLI APT public key:
   ```shell
   sudo mkdir -p /etc/apt/keyrings
   curl https://packages.confluent.io/confluent-cli/deb/archive.key | sudo gpg --dearmor -o /etc/apt/keyrings/confluent-cli.gpg
   sudo chmod go+r /etc/apt/keyrings/confluent-cli.gpg
   ```

   You should see output similar to the following:
   ```text
   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                       Dload  Upload   Total   Spent    Left  Speed
   100  3106  100  3106    0     0  16062      0 --:--:-- --:--:-- --:--:-- 16010
   ```
3. Add the Confluent CLI repository to your APT configuration:
   ```shell
   echo "deb [signed-by=/etc/apt/keyrings/confluent-cli.gpg] https://packages.confluent.io/confluent-cli/deb stable main" | sudo tee /etc/apt/sources.list.d/confluent-cli.list >/dev/null
   ```
4. Update `apt`:
   ```bash
   sudo apt update
   ```
5. Install the Confluent CLI:
   ```bash
   sudo apt install confluent-cli
   ```

   You should see output similar to:
   ```text
   ...
   The following NEW packages will be installed:
   confluent-cli
   0 upgraded, 1 newly installed, 0 to remove and 41 not upgraded.
   Need to get 19.3 MB of archives.
   After this operation, 56.2 MB of additional disk space will be used.
   Get:1 https://packages.confluent.io/confluent-cli/deb stable/main amd64 confluent-cli amd64 3.48.0 [19.3 MB]
   ...
   Unpacking confluent-cli (3.48.0) ...
   Setting up confluent-cli (3.48.0) ...
   ```

**Confluent Platform**

If you installed Confluent Platform using APT, you should already have a version of the
Confluent CLI. In most cases, Confluent Platform users should use the version of
Confluent CLI provided with Confluent Platform. However, you can still install the latest
version of the Confluent CLI from the CLI repository by using the following
steps:

1. Install `curl` and `gpg` (if you have not already installed them).
   ```shell
   sudo apt install curl gnupg
   ```
2. Install the Confluent CLI APT public key:
   ```shell
   sudo mkdir -p /etc/apt/keyrings
   curl https://packages.confluent.io/confluent-cli/deb/archive.key | sudo gpg --dearmor -o /etc/apt/keyrings/confluent-cli.gpg
   sudo chmod go+r /etc/apt/keyrings/confluent-cli.gpg
   ```

   You should see output similar to the following:
   ```text
    % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                        Dload  Upload   Total   Spent    Left  Speed
    100  3106  100  3106    0     0  16062      0 --:--:-- --:--:-- --:--:-- 16010
   ```
3. Add the Confluent CLI repository to your APT configuration:
   ```shell
   echo "deb [signed-by=/etc/apt/keyrings/confluent-cli.gpg] https://packages.confluent.io/confluent-cli/deb stable main" | sudo tee /etc/apt/sources.list.d/confluent-cli.list >/dev/null
   ```
4. Update `apt`:
   ```bash
   sudo apt update
   ```
5. Install the latest version of the Confluent CLI. You must provide
   a specific CLI version as shown in the following example. Otherwise,
   APT installs the CLI version bundled with Confluent Platform, which uses the Confluent Platform version number
   instead of the CLI version number.
   ```bash
   sudo apt install confluent-cli=3.48.0
   ```

   To find the current latest version, you can run the following commands:
   `sudo apt update` and `sudo apt list -a confluent-cli` and look for
   the highest version number earlier than `7.x` or refer to the
   [Confluent CLI Release Notes](https://docs.confluent.io/confluent-cli/current/release-notes.html).

#### NOTE
Updating the CLI or installing Confluent Platform through APT
replaces this version of the CLI with the version provided by Confluent Platform.

### YUM

RHEL and CentOS users can install the latest version of Confluent CLI using
the YUM package manager.

1. Install the Confluent CLI YUM public key:
   ```bash
   sudo rpm --import https://packages.confluent.io/confluent-cli/rpm/archive.key
   ```
2. Install `yum-config-manager` (included in the `yum-utils` package) if it
   is not already installed:
   ```bash
   sudo yum install yum-utils
   ```
3. Add the Confluent CLI repository to your YUM configuration:
   ```bash
   yum-config-manager --add-repo https://packages.confluent.io/confluent-cli/rpm/confluent-cli.repo
   ```

   You should see output similar to:
   ```text
   Loaded plugins: fastestmirror, ovl
   adding repo from: https://packages.confluent.io/confluent-cli/rpm/confluent-cli.repo
   grabbing file https://packages.confluent.io/confluent-cli/rpm/confluent-cli.repo to /etc/yum.repos.d/confluent-cli.repo
   repo saved to /etc/yum.repos.d/confluent-cli.repo
   ```
4. Clear the YUM caches:
   ```bash
   sudo yum clean all
   ```

   You should see output similar to:
   ```text
   Loaded plugins: fastestmirror, ovl
   Cleaning repos: Confluent-CLI base endpoint extras updates
   Cleaning up list of fastest mirrors
   ```
5. Install the Confluent CLI:
   ```bash
   sudo yum install confluent-cli
   ```

   You should see output similar to:
   ```text
   Loaded plugins: fastestmirror, ovl
   Determining fastest mirrors
   * base: centos-distro.1gservers.com
   * extras: mirror.keystealth.org
   * updates: mirrors.unifiedlayer.com
   Confluent-CLI
   base
   endpoint
   extras
   updates
   (1/6): base/7/x86_64/group_gz
   (2/6): extras/7/x86_64/primary_db
   (3/6): Confluent-CLI/primary_db
   (4/6): endpoint/7/x86_64/primary_db
   (5/6): base/7/x86_64/primary_db
   (6/6): updates/7/x86_64/primary_db
   Resolving Dependencies
   --> Running transaction check
   ---> Package confluent-cli.x86_64 0:3.48.0-1 will be installed
   --> Finished Dependency Resolution

   Dependencies Resolved

   ========================================================================================================================================================================================================================
   Package                                                      Arch                           Version                            Repository                                               Size
   ========================================================================================================================================================================================================================
   Installing:
   confluent-cli                                                x86_64                         3.48.0-1                           Confluent-CLI                                            19 M

   Transaction Summary
   ========================================================================================================================================================================================================================
   Install  1 Package

   Total download size: 19 M
   Installed size: 54 M
   Is this ok [y/d/N]: y
   Downloading packages:
   confluent-cli-3.48.0-1.x86_64.rpm
   Running transaction check
   Running transaction test
   Transaction test succeeded
   Running transaction
   Verifying  : confluent-cli-3.48.0-1.x86_64

   Installed:
   confluent-cli.x86_64 0:3.48.0-1

   Complete!
   ```

**Confluent Platform**

If you installed Confluent Platform using YUM, you should already have a version of the
Confluent CLI. In most cases, Confluent Platform users should use the version of
Confluent CLI provided with Confluent Platform. However, if you want to install the latest
version of the Confluent CLI from the CLI repository, you can use the
following steps:

1. Install the Confluent CLI YUM public key:
   ```text
   sudo rpm --import https://packages.confluent.io/confluent-cli/rpm/archive.key
   ```
2. Add the Confluent CLI repository to your YUM configuration:
   ```text
   yum-config-manager --add-repo https://packages.confluent.io/confluent-cli/rpm/confluent-cli.repo
   ```
3. Uninstall the existing version of the Confluent CLI. This also
   uninstalls `confluent-platform`, but not the individual packages
   included with Confluent Platform:
   ```bash
   sudo yum remove confluent-cli
   ```

   You should see output similar to:
   ```text
   Loaded plugins: fastestmirror, ovl
   Resolving Dependencies
   --> Running transaction check
   ---> Package confluent-cli.x86_64 0:7.5.3-1 will be erased
   --> Processing Dependency: confluent-cli = 7.5.3 for package: confluent-platform-7.5.3-1.noarch
   --> Running transaction check
   ---> Package confluent-platform.noarch 0:7.5.3-1 will be erased
   --> Finished Dependency Resolution

   Dependencies Resolved

   =============================================================================================================================================================================================================
   Package                                                        Arch                          Version                                 Repository                                Size
   =============================================================================================================================================================================================================
   Removing:
   confluent-cli                                                  x86_64                        7.5.3-1                                 @Confluent                                208 M
   Removing for dependencies:
   confluent-platform                                             noarch                        7.5.3-1                                 @Confluent                                0.0

   Transaction Summary
   =============================================================================================================================================================================================================
   Remove  1 Package (+1 Dependent package)

   Installed size: 208 M
   Is this ok [y/N]: y
   Downloading packages:
   Running transaction check
   Running transaction test
   Transaction test succeeded
   Running transaction
   Erasing    : confluent-platform-7.5.3-1.noarch
   Erasing    : confluent-cli-7.5.3-1.x86_64
   Verifying  : confluent-platform-7.5.3-1.noarch
   Verifying  : confluent-cli-7.5.3-1.x86_64

   Removed:
   confluent-cli.x86_64 0:7.5.3-1

   Dependency Removed:
   confluent-platform.noarch 0:7.5.3-1

   Complete!
   ```
4. Clear the YUM caches:
   ```text
   sudo yum clean all
   ```

   You should see output similar to:
   ```text
   Loaded plugins: fastestmirror, ovl
   Cleaning repos: Confluent-CLI base endpoint extras updates
   Cleaning up list of fastest mirrors
   ...
   ```
5. Install the standalone Confluent CLI:
   ```text
   sudo yum --disablerepo=Confluent install confluent-cli
   ```

   This command assumes that users have added the Confluent Platform repository using the
   `confluent.repo` file provided in [Install Confluent Platform using Systemd
   on RHEL and CentOS](https://docs.confluent.io/platform/current/installation/installing_cp/rhel-centos.html#install-cp-using-systemd-on-rhel-and-centos).
   If you modified the repository ID, you must provide the ID as
   the argument to `--disablerepo` in place of `Confluent` in the
   previous step. You can view repository IDs and names using
   `yum repolist all`.

#### NOTE
Updating the CLI or installing Confluent Platform through YUM
replaces this version of the CLI with the version provided by Confluent Platform.

### Windows

To install the Confluent CLI on Windows, complete the following
steps:

1. Download the latest Windows ZIP file from
   `https://github.com/confluentinc/cli/releases/latest`.
2. Unzip the following file:
   ```bash
   confluent_<version>_windows_amd64.zip
   ```
3. Run `confluent.exe`.

<a id="other-cli-install-methods"></a>

## Other installation methods

This section includes other methods you can use to install the Confluent CLI.

### Docker

To install the Confluent CLI on Docker Desktop, run the following command to
pull the latest CLI version:

```bash
docker pull confluentinc/confluent-cli:latest
```

You can also install a specific version:

```bash
docker pull confluentinc/confluent-cli:<version>
```

<a id="confluent-cli-install-with-cp"></a>

### Confluent Platform installation package

Confluent Platform installation packages include the Confluent CLI binaries for each of the
operating systems and architectures that the Confluent CLI supports.

Confluent Community software users must download the Confluent CLI
separately and configure it manually.

To use the Confluent CLI in the Confluent Platform package:

1. Set the Confluent Platform home environment variable:
   ```bash
   export CONFLUENT_HOME=<confluent_install_dir>
   ```
2. Add the location of the CLI to the `PATH`:
   ```bash
   export PATH=$CONFLUENT_HOME/bin:$PATH
   ```

<a id="confluent-cli-version-install"></a>

#### Install alternative version in Confluent Platform package

The version of the Confluent CLI used by Confluent Platform can be changed by downloading a
specific Confluent CLI binary and using it to replace the current binary.

When you download and install the Confluent CLI outside of the Confluent Platform package,
ensure you install a Confluent CLI version that is compatible with the version
of Confluent Platform you are running. For reference, see the [Confluent CLI to Confluent Platform compatibility table](/platform/current/installation/versions-interoperability.html#confluent-cli-cp-compatibility).

1. Download the appropriate version of the Confluent CLI.
2. Use the downloaded binary to replace the existing Confluent CLI binary
   located in subdirectories of `$CONFLUENT_HOME/libexec/cli/`.

   For example, on macOS, which is the `darwin` operating system and
   `amd64` architecture:
   ```bash
   cp <cli_binaries> $CONFLUENT_HOME/libexec/cli/darwin_amd64/
   ```

<a id="confluent-cli-bundle-install"></a>

### Tarball or ZIP installation

1. Download and install the most recently released CLI binaries for your
   platform:
   - [macOS with 64-bit Intel chips (Darwin AMD64)](https://packages.confluent.io/confluent-cli/archives/latest/confluent_darwin_amd64.tar.gz)
   - [macOS with Apple chips (Darwin ARM64)](https://packages.confluent.io/confluent-cli/archives/latest/confluent_darwin_arm64.tar.gz)
   - [Windows with 64-bit Intel or AMD chips (Windows AMD64)](https://packages.confluent.io/confluent-cli/archives/latest/confluent_windows_amd64.zip)
   - [Linux with 64-bit Intel or AMD chips (Linux AMD64) (glibc)](https://packages.confluent.io/confluent-cli/archives/latest/confluent_linux_amd64.tar.gz)
   - [Linux with 64-bit ARM chips (Linux ARM64) (glibc)](https://packages.confluent.io/confluent-cli/archives/latest/confluent_linux_arm64.tar.gz)
   - [Alpine with 64-bit Intel or AMD chips (Alpine AMD64) (musl)](https://packages.confluent.io/confluent-cli/archives/latest/confluent_alpine_amd64.tar.gz)
   - [Alpine with 64-bit ARM chips (Alpine ARM64) (musl)](https://packages.confluent.io/confluent-cli/archives/latest/confluent_alpine_arm64.tar.gz)
   - [Checksums (operating system agnostic)](https://packages.confluent.io/confluent-cli/archives/latest/confluent_checksums.txt)
2. Set the `PATH` environment to include the directory that you downloaded the
   CLI binaries in the previous step:
   ```bash
   export PATH=<path_to_cli>:$PATH
   ```
3. Optionally, if you do not have enough space in the default directory that
   the CLI stores logs and data, set the `CONFLUENT_CURRENT` environment
   variable to use a different directory:
   ```bash
   export CONFLUENT_CURRENT=<path_to_confluent_local_data>
   ```

## Verify the Confluent CLI installation

You can confirm the version and the operating system (OS) of the CLI
with the following command:

```text
confluent version
```

The output of this command varies depending on your version and OS. For
example, on macOS, the output resembles the following:

```text
confluent - Confluent CLI

Version:     v4.43.0
Git Ref:     14b42e02
Build Date:  2025-10-24T21:09:49Z
Go Version:  go1.24.6 (darwin/arm64)
Development: false
```

<a id="cli-upgrade-instructions"></a>

## Update the Confluent CLI

Use the `confluent update` command to update from an earlier version of the
Confluent CLI to a newer version. For the full syntax, see [confluent update](command-reference/confluent_update.md#confluent-update).

To ensure compatibility, updates using the `confluent update` command are
disabled for the CLI packaged with Confluent Platform. If you need to update to a later
version of the CLI, see [Install alternative version in Confluent Platform package](#confluent-cli-version-install).

## Uninstall the Confluent CLI

Methods for uninstalling the Confluent CLI vary depending on your
operating system and installation method (package manager or a direct
binary download).

### macOS

If you used Homebrew on macOS to install the CLI, you can remove it
using the standard uninstall command:

```bash
brew uninstall confluentinc/tap/cli
```

### APT or YUM

If installed with a Linux (APT or YUM) package manager, the uninstall
process varies depending on the OS and package manager you used.
For installations done through the Confluent repository, use your system’s package manager.

- Ubuntu/Debian (APT):
  ```bash
  sudo apt-get remove confluent-cli
  # To remove unused dependencies as well:
  sudo apt-get autoremove
  ```
- RHEL/CentOS/Fedora (YUM/DNF):
  ```bash
  sudo yum remove confluent-cli
  ```

  Or (for Fedora)
  ```bash
  sudo dnf remove confluent-cli
  ```

### Script or Binary (Manual install)

If you installed the CLI using the curl script or by downloading the
binary manually, you need to delete the binary and its configuration
directory.

1. Locate and remove the binary: find where the binary is located
   (usually `/usr/local/bin` or a local bin folder) and delete it.
   ```bash
   which confluent
   # This will show you the path, e.g., /usr/local/bin/confluent
   rm /usr/local/bin/confluent
   ```
2. Remove the configuration directory:
   ```bash
   rm -rf ~/.confluent/
   ```

If you installed the CLI as part of Confluent Platform, you should uninstall the platform package itself:

- Ubuntu:
  ```bash
  sudo apt-get remove confluent-platform
  ```
- RHEL:
  ```bash
  sudo yum remove confluent-platform
  ```
- Fedora:
  ```bash
  sudo dnf remove confluent-platform
  ```

### Windows

If you installed the CLI using the Windows native installer, do the
following to uninstall it:

1. Delete the executable.

   Since you manually unzipped the file, locate the `confluent.exe`
   file and delete it. Check your **Downloads** folder or wherever you
   extracted the ZIP. If you moved `confluent.exe` to a permanent
   folder, such as `C:\tools` or `C:\bin`, delete that folder.
2. Remove the CLI Configuration (required).

   The CLI creates a hidden folder to store your login sessions,
   environments, and cluster metadata. Even if you delete
   `confluent.exe`, these files stay on your hard drive.
   1. Open File Explorer.
   2. In the address bar, paste: `%USERPROFILE%` and hit Enter.
   3. Find the folder named `.confluent`, and delete it.
3. Clean up the System Path.

   If you followed common practices, you likely added the folder
   containing `confluent.exe` to your Windows `Path` so you could
   run it from any terminal. Remove this folder to keep your
   system clean.
   1. Press the Windows Key and type `env`.
   2. Select **Edit the system environment variables**.
   3. Click **Environment Variables**.
   4. In the **User variables** section, find the variable named **Path**
      and click **Edit**.
   5. Look for the folder path where you unzipped the Confluent CLI.
   6. Select that line and click **Delete**.
   7. Click **OK** on all windows to save.
4. Verify it’s uninstalled.

   The changes don’t appear in an already open window.
   Open a new command prompt or PowerShell window and type:
   ```bash
   confluent version
   ```

   If the CLI is uninstalled correctly, you should see an error message similar to:
   ```text
   'confluent' is not recognized as an internal or external command...
   ```

## Confluent Platform properties files

The following list includes the default configuration properties files for
Confluent Platform services, where `$CONFLUENT_HOME` is the directory with Confluent Platform installed.
You reference or modify the appropriate file when you work with a Confluent Platform
service.

- Connect: `$CONFLUENT_HOME/etc/schema-registry/connect-avro-distributed.properties`
- Control Center: `$C3_HOME/etc/confluent-control-center/control-center-dev.properties` <sup>[1](#f1)</sup>
- KRaft Controller: `$CONFLUENT_HOME/etc/kafka/controller.properties`
- Apache Kafka® (KRaft mode): `$CONFLUENT_HOME/etc/kafka/broker.properties`
- Kafka (ZooKeeper mode, Legacy): `$CONFLUENT_HOME/etc/kafka/server.properties`
- REST Proxy: `$CONFLUENT_HOME/etc/kafka-rest/kafka-rest.properties`
- ksqlDB: `$CONFLUENT_HOME/etc/ksqldb/ksql-server.properties`
- Schema Registry: `$CONFLUENT_HOME/etc/schema-registry/schema-registry.properties`
- ZooKeeper: `$CONFLUENT_HOME/etc/kafka/zookeeper.properties`

* <a id='f1'>**[1]**</a> Starting with Confluent Platform 8.0, Control Center is provided in an independent release, as described in [Control Center single-node manual installation](/control-center/current/installation/overview.html#single-node-manual-installation), and the Control Center examples in this tutorial: [Getting Started with a multi-broker cluster](/platform/current/get-started/tutorial-multi-broker.html#optional-install-and-configure-c3). In previous versions of Confluent Platform, this path was `$CONFLUENT_HOME/etc/confluent-control-center/control-center-dev.properties`.


<a id="confluent-api-key-create"></a>

# confluent api-key create

## Description

Create API keys for a given resource. A resource is a Confluent product or service for which an API key can be created. Specify a Kafka cluster ID (for example, lkc-abc123) for the –resource parameter to create a Kafka cluster API key, a Schema Registry cluster ID (for example, lsrc-abc123) to create a Schema Registry API key, or a ksqlDB cluster ID (for example, lksqlc-abc123) to create a ksqlDB API key. To create a Flink region API key, specify “flink” along with the –environment and –region flags. To create a Tableflow API key, specify “tableflow”, or specify “cloud” to create a Cloud resource management API key. To create a Global API key that can be used across all supported Confluent Cloud resources, specify “global”.

```none
confluent api-key create [flags]
```

## Flags

```none
    --resource string          REQUIRED: The ID of the resource the API key is for. Use "cloud" for a Cloud API key, "global" for a Global API key, "flink" for a Flink API key, or "tableflow" for a Tableflow API key.
    --description string       Description of API key.
    --cloud string             Specify the cloud provider as "aws", "azure", or "gcp".
    --region string            Cloud region for Flink (use "confluent flink region list" to see all).
    --use                      Use the created API key for the provided resource.
    --context string           CLI context name.
    --environment string       Environment ID.
    --service-account string   Service account ID.
-o, --output string            Specify the output format as "human", "json", or "yaml". (default "human")
```

## Global Flags

```none
-h, --help            Show help for this command.
    --unsafe-trace    Equivalent to -vvvv, but also log HTTP requests and responses which might contain plaintext secrets.
-v, --verbose count   Increase verbosity (-v for warn, -vv for info, -vvv for debug, and -vvvv for trace).
```

## Examples

Create a Cloud API key:

```none
confluent api-key create --resource cloud
```

Create a Global API key:

```none
confluent api-key create --resource global
```

Create a Flink API key for region “N. Virginia (us-east-1)”:

```none
confluent api-key create --resource flink --cloud aws --region us-east-1
```

Create an API key with full access to Kafka cluster “lkc-123456”:

```none
confluent api-key create --resource lkc-123456
```

Create an API key for Kafka cluster “lkc-123456” and service account “sa-123456”:

```none
confluent api-key create --resource lkc-123456 --service-account sa-123456
```

Create an API key for Schema Registry cluster “lsrc-123456”:

```none
confluent api-key create --resource lsrc-123456
```

Create an API key for KSQL cluster “lksqlc-123456”:

```none
confluent api-key create --resource lksqlc-123456
```

Create a Tableflow API key:

```none
confluent api-key create --resource tableflow
```

## See Also

* [confluent api-key](index.md#confluent-api-key) - Manage API keys.

<a id="confluent-cli-plugins"></a>

# Extend the Confluent CLI with Plugins

Confluent CLI plugins enable you to extend the capabilities of the
Confluent CLI to interact with Confluent resources. You can create simple and
complex scripting workflows using the CLI and plugins.

To use plugins, you must have [Confluent CLI installed](install.md#cli-install). Note
that plugins may or may not be enabled by default depending on the environment
you are operating in:

- **macOS and Linux users**: Confluent CLI plugins are enabled by default. If
  you have a large `$PATH` and plugins take too long to index, you can opt
  out by adding `"disable_plugins": true` to your configuration file at
  `$HOME/.confluent/config.json`.
- **Windows users**: Confluent CLI plugins are disabled by default. You can
  manually re-enable plugins in the `~/.confluent/config.json` file.

## Plugin repository

You can find contributed plugins for use with the Confluent CLI in Confluent’s dedicated [GitHub repository](https://github.com/confluentinc/cli-plugins). You can also contribute a plugin for others to leverage as well. To do so, follow the steps to [add a plugin](https://github.com/confluentinc/cli-plugins/blob/main/CONTRIBUTING.md).

## Discover plugins

Plugins are user-created and are not included with the Confluent CLI. Use the
`confluent plugin list` command to search your `PATH` for plugin
executables. This command lists plugin names alongside their file paths in the
order in which they are discovered.

## Install a Plugin

To install and use a plugin:

1. Make the plugin file executable:
   ```bash
   sudo chmod +x <plugin file>
   ```
2. Place the plugin file on your `PATH`.
3. Execute the plugin.

   Note that plugin executables inherit the environment settings from the
   Confluent CLI.

## Disable plugins

The Confluent CLI plugins feature is enabled by default. To disable the plugin
feature, add the following in the configuration file,
`~/.confluent/config.json`:

```json
"disable_plugins": true
```

## Write a plugin

You can write a plugin in any programming or scripting language that allows you
to write terminal commands.

### Plugin file name

A plugin’s command name is determined by its filename. The following rules apply:

- A plugin filename must begin with `confluent-`.
- Subcommands in a plugin’s command are separated by dashes (`-`) in its
  filename. For example, a plugin named `confluent-this-command` would
  define the command `confluent this command`.
- To have a plugin command containing dashes (`-`) or underscores (`_`), use
  an underscore (`_`) in the plugin filenames in place of a dash (`-`). For
  example, you can invoke a plugin whose filename is `confluent-that_command`
  by running either of the following commands:
  ```text
  confluent that-command
  ```

  ```text
  confluent that_command
  ```
- On Windows, all file extensions defined in `$PATHTEXT` are supported.
- On Linux and macOS, any file extension is supported as long as the file is
  executable.

#### Naming limitations

The following limitations apply to naming plugins. If these rules are violated,
the `confluent plugin list` command output will have a warning message that
the offending plugin will be ignored.

- A plugin can’t override an existing command. Therefore, a plugin whose name
  exactly matches a native CLI command’s name will be ignored.
- Two or more plugins can’t have the same name.

  The first one found on your `$PATH` is used. The other plugins
  discovered with the same name are ignored.

### Plugin flags and arguments

If the user invokes a plugin and passes in additional arguments and/or flags, it
is the plugin’s responsibility to validate and parse them, as the CLI will
pass in arguments and flags as-is.

For example, when running `confluent example arg1 --flag=val arg2`, the CLI will:

1. Look for the plugin with the longest possible name,
   `confluent-example-arg1`.
2. Treat the last dash-separated value as an argument and try to find the next
   longest possible name, `confluent-example`–since the
   `confluent-example-arg1` plugin is not found.
3. Repeat the search process until either a plugin is found or there are no more
   dash-separated values besides `confluent-`–meaning that no plugins matching
   the command have been found.
4. Invoke the found plugin and pass all arguments and flags after the plugin’s
   name (`arg1 --flag=val arg2`) as arguments to the plugin process, since
   `confluent-example` exists.

## Example

To list Kafka clusters in all environments:

1. Create a plugin file called `confluent-kafka-cluster-list_all`:
   ```bash
   #!/bin/bash
   for env_id in $(confluent environment list -o json | jq -r '.[].id');
   do
     confluent kafka cluster list --environment $env_id
   done
   ```
2. Make the plugin file executable:
   ```bash
   sudo chmod +x confluent-kafka-cluster-list_all
   ```
3. Place the plugin file in your `PATH`.
4. Ensure the plugin has been discovered by the Confluent CLI:
   ```text
   confluent plugin list
              Plugin Name           |                    File Path
   ---------------------------------+--------------------------------------------------
     confluent kafka cluster        | /usr/local/bin/confluent-kafka-cluster-list_all
     list-all                       |
   ```
5. Execute the plugin.
   ```text
   confluent kafka cluster list-all
          ID      |   Name    | Type  | Provider |  Region   | Availability | Status
   ---------------+-----------+-------+----------+-----------+--------------+---------
       lkc-j9v1yw | cluster_0 | BASIC | aws      | us-east-1 | single-zone  | UP
          ID      |   Name    | Type  | Provider |  Region   | Availability | Status
   ---------------+-----------+-------+----------+-----------+--------------+---------
       lkc-rj09ok | cluster_1 | BASIC | aws      | us-east-1 | single-zone  | UP
   ```


<a id="confluent-completion"></a>

# confluent completion

## Description

Use this command to print the shell completion
code for the specified shell (Bash/Zsh only). The shell code must be evaluated to provide
interactive completion of `confluent` commands.

Install Bash completions on macOS:
: 1. Install Homebrew ([https://brew.sh/](https://brew.sh/)).
  2. Install Bash completions using the `brew` command:
     ```none
     brew install bash-completion
     ```
  3. Update your Bash profile:
     ```none
     echo '[[ -r "$(brew --prefix)/etc/profile.d/bash_completion.sh" ]] && . "$(brew --prefix)/etc/profile.d/bash_completion.sh"' >> ~/.bash_profile
     ```
  4. Run the following command to install auto completion:
     ```none
     confluent completion bash > $(brew --prefix)/etc/bash_completion.d/confluent
     ```

Install Bash completions on Linux:
: 1. Install Bash completion:
     ```none
     sudo apt-get install bash-completion
     ```
  2. Set the `confluent completion` code for Bash to a file that’s sourced on login:
     ```none
     confluent completion bash > /etc/bash_completion.d/confluent
     ```
  3. Load the `confluent completion` code for Bash into the current shell:
     ```none
     source /etc/bash_completion.d/confluent
     ```
  4. Add the source command above to your `~/.bashrc` or `~/.bash_profile` to enable completions for new terminals.

Install Zsh completions:
: Zsh looks for completion functions in the directories listed in the `fpath` shell variable.
  <br/>
  1. Put the `confluent completion` code for Zsh into a file in one the `fpath` directories, preferably one of the functions directories. For example:
     ```none
     confluent completion zsh > ${fpath[1]}/_confluent
     ```
  2. Enable Zsh completions:
     ```none
     autoload -U compinit && compinit
     ```
  3. Add the autoload command in your `~/.zshrc` to enable completions for new terminals. If you encounter error messages about insecure files, you can resolve by running the `chown` command to change the `_confluent` file to the same `user:group` as the other files in `${fpath[1]}/`.

```none
confluent completion <bash|zsh> [flags]
```

## Global Flags

```none
-h, --help            Show help for this command.
    --unsafe-trace    Equivalent to -vvvv, but also log HTTP requests and responses which might contain plaintext secrets.
-v, --verbose count   Increase verbosity (-v for warn, -vv for info, -vvv for debug, and -vvvv for trace).
```

## See Also

* [Confluent CLI Command Reference](index.md#confluent-ref) - Confluent CLI.

