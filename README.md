# switch-tool


  This script creates switches between the versions of various tools,
  found in /mnt/jqa/sw/tools/ (curently hard-coded).

  ## Usage:
  
    ```
    $ switch maven 2.1.0
    $ mvn ...
    ```

  ## Installation:
   * Set PATH to begin with ~/sw/tools/.links (in ~/.bashrc)

  ## Tools directory structure:
  
   * .../<tool_name>/
     * <tool_version>/
     * <tool_version2>/
     * onSwitch.sh
     * onRun.sh

  ## Callback scripts:

   * onSwitch.sh - called when the version switch is performed.
     * Called using:   . onSwitch.sh <tool_name> <tool_version>

   * onRun.sh - if present, all tool's runnables will be called through a script,
                which will be re-created each time the versions are switched:

          TOOL_NAME=<tool_name>    # Few variables are set at the top of the script.
          TOOL_VERSION=<...>       # 1.2.3
          TOOL_HOME=<...>          # Tool home dir - i.e., the dir particular version.
          TOOL_RUNNABLE_PATH=<...> # Path to the runnable to be called. 

          <content of onRun.sh>    # The content is simply pasted here.
          <tool_runnable> $@       # Calls the current version of the tool runnable.

  ## Todo:
   * Upon switch, remove links created with previous switch.
     * All that belong to the tools/<tool_name> dir (parse the variables at the top of the scripts)

  ## History
  
  2009-12-22:
   * Runnables are now searched automatically in TOOL_HOME/bin if there's no runnables.txt.
   * Softlinks to executable files also count as runnables.
   * Home dir of this script is detected automatically.
   * Meta-dirs now start with a dot (.links, .homes, .template).


