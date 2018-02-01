# am 相关命令

```sh
usage: am [subcommand] [options]
usage: am start [-D] [-W] [-P <FILE>] [--start-profiler <FILE>]
               [--sampling INTERVAL] [-R COUNT] [-S] [--opengl-trace]
               [--user <USER_ID> | current] <INTENT>
       am startservice [--user <USER_ID> | current] <INTENT>
       am stopservice [--user <USER_ID> | current] <INTENT>
       am force-stop [--user <USER_ID> | all | current] <PACKAGE>
       am kill [--user <USER_ID> | all | current] <PACKAGE>
       am kill-all
       am broadcast [--user <USER_ID> | all | current] <INTENT>
       am instrument [-r] [-e <NAME> <VALUE>] [-p <FILE>] [-w]
               [--user <USER_ID> | current]
               [--no-window-animation] [--abi <ABI>] <COMPONENT>
       am profile start [--user <USER_ID> current] [--sampling INTERVAL] <PROCESS> <FILE>
       am profile stop [--user <USER_ID> current] [<PROCESS>]
       am dumpheap [--user <USER_ID> current] [-n] <PROCESS> <FILE>
       am set-debug-app [-w] [--persistent] <PACKAGE>
       am clear-debug-app
       am set-watch-heap <PROCESS> <MEM-LIMIT>
       am clear-watch-heap
       am monitor [--gdb <port>]
       am hang [--allow-restart]
       am restart
       am idle-maintenance
       am screen-compat [on|off] <PACKAGE>
       am package-importance <PACKAGE>
       am to-uri [INTENT]
       am to-intent-uri [INTENT]
       am to-app-uri [INTENT]
       am switch-user <USER_ID>
       am start-user <USER_ID>
       am stop-user [-w] <USER_ID>
       am stack start <DISPLAY_ID> <INTENT>
       am stack movetask <TASK_ID> <STACK_ID> [true|false]
       am stack resize <STACK_ID> <LEFT,TOP,RIGHT,BOTTOM>
       am stack split <STACK_ID> <v|h> [INTENT]
       am stack list
       am stack info <STACK_ID>
       am task lock <TASK_ID>
       am task lock stop
       am task resizeable <TASK_ID> [true|false]
       am task resize <TASK_ID> <LEFT,TOP,RIGHT,BOTTOM>
       am get-config
       am set-inactive [--user <USER_ID>] <PACKAGE> true|false
       am get-inactive [--user <USER_ID>] <PACKAGE>
       am send-trim-memory [--user <USER_ID>] <PROCESS>
               [HIDDEN|RUNNING_MODERATE|BACKGROUND|RUNNING_LOW|MODERATE|RUNNING_CRITICAL|COMPLETE]

am start: start an Activity.  Options are:
    -D: enable debugging
    -W: wait for launch to complete
    --start-profiler <FILE>: start profiler and send results to <FILE>
    --sampling INTERVAL: use sample profiling with INTERVAL microseconds
        between samples (use with --start-profiler)
    -P <FILE>: like above, but profiling stops when app goes idle
    -R: repeat the activity launch <COUNT> times.  Prior to each repeat,
        the top activity will be finished.
    -S: force stop the target app before starting the activity
    --opengl-trace: enable tracing of OpenGL functions
    --user <USER_ID> | current: Specify which user to run as; if not
        specified then run as the current user.

am startservice: start a Service.  Options are:
    --user <USER_ID> | current: Specify which user to run as; if not
        specified then run as the current user.

am stopservice: stop a Service.  Options are:
    --user <USER_ID> | current: Specify which user to run as; if not
        specified then run as the current user.

am force-stop: force stop everything associated with <PACKAGE>.
    --user <USER_ID> | all | current: Specify user to force stop;
        all users if not specified.

am kill: Kill all processes associated with <PACKAGE>.  Only kills.
  processes that are safe to kill -- that is, will not impact the user
  experience.
    --user <USER_ID> | all | current: Specify user whose processes to kill;
        all users if not specified.

am kill-all: Kill all background processes.

am broadcast: send a broadcast Intent.  Options are:
    --user <USER_ID> | all | current: Specify which user to send to; if not
        specified then send to all users.
    --receiver-permission <PERMISSION>: Require receiver to hold permission.

am instrument: start an Instrumentation.  Typically this target <COMPONENT>
  is the form <TEST_PACKAGE>/<RUNNER_CLASS>.  Options are:
    -r: print raw results (otherwise decode REPORT_KEY_STREAMRESULT).  Use with
        [-e perf true] to generate raw output for performance measurements.
    -e <NAME> <VALUE>: set argument <NAME> to <VALUE>.  For test runners a
        common form is [-e <testrunner_flag> <value>[,<value>...]].
    -p <FILE>: write profiling data to <FILE>
    -w: wait for instrumentation to finish before returning.  Required for
        test runners.
    --user <USER_ID> | current: Specify user instrumentation runs in;
        current user if not specified.
    --no-window-animation: turn off window animations while running.
    --abi <ABI>: Launch the instrumented process with the selected ABI.
        This assumes that the process supports the selected ABI.

am profile: start and stop profiler on a process.  The given <PROCESS> argument
  may be either a process name or pid.  Options are:
    --user <USER_ID> | current: When supplying a process name,
        specify user of process to profile; uses current user if not specified.

am dumpheap: dump the heap of a process.  The given <PROCESS> argument may
  be either a process name or pid.  Options are:
    -n: dump native heap instead of managed heap
    --user <USER_ID> | current: When supplying a process name,
        specify user of process to dump; uses current user if not specified.

am set-debug-app: set application <PACKAGE> to debug.  Options are:
    -w: wait for debugger when application starts
    --persistent: retain this value

am clear-debug-app: clear the previously set-debug-app.

am set-watch-heap: start monitoring pss size of <PROCESS>, if it is at or
    above <HEAP-LIMIT> then a heap dump is collected for the user to report

am clear-watch-heap: clear the previously set-watch-heap.

am bug-report: request bug report generation; will launch UI
    when done to select where it should be delivered.

am monitor: start monitoring for crashes or ANRs.
    --gdb: start gdbserv on the given port at crash/ANR

am hang: hang the system.
    --allow-restart: allow watchdog to perform normal system restart

am restart: restart the user-space system.

am idle-maintenance: perform idle maintenance now.

am screen-compat: control screen compatibility mode of <PACKAGE>.

am package-importance: print current importance of <PACKAGE>.

am to-uri: print the given Intent specification as a URI.

am to-intent-uri: print the given Intent specification as an intent: URI.

am to-app-uri: print the given Intent specification as an android-app: URI.

am switch-user: switch to put USER_ID in the foreground, starting
  execution of that user if it is currently stopped.

am start-user: start USER_ID in background if it is currently stopped,
  use switch-user if you want to start the user in foreground.

am stop-user: stop execution of USER_ID, not allowing it to run any
  code until a later explicit start or switch to it.
  -w: wait for stop-user to complete.

am stack start: start a new activity on <DISPLAY_ID> using <INTENT>.

am stack movetask: move <TASK_ID> from its current stack to the top (true) or   bottom (false) of <STACK_ID>.

am stack resize: change <STACK_ID> size and position to <LEFT,TOP,RIGHT,BOTTOM>.

am stack split: split <STACK_ID> into 2 stacks <v>ertically or <h>orizontally
   starting the new stack with [INTENT] if specified. If [INTENT] isn't
   specified and the current stack has more than one task, then the top task
   of the current task will be moved to the new stack. Command will also force
   all current tasks in both stacks to be resizeable.

am stack list: list all of the activity stacks and their sizes.

am stack info: display the information about activity stack <STACK_ID>.

am task lock: bring <TASK_ID> to the front and don't allow other tasks to run.

am task lock stop: end the current task lock.

am task resizeable: change if <TASK_ID> is resizeable (true) or not (false).

am task resize: makes sure <TASK_ID> is in a stack with the specified bounds.
   Forces the task to be resizeable and creates a stack if no existing stack
   has the specified bounds.

am get-config: retrieve the configuration and any recent configurations
  of the device.

am set-inactive: sets the inactive state of an app.

am get-inactive: returns the inactive state of an app.

am send-trim-memory: Send a memory trim event to a <PROCESS>.

<INTENT> specifications include these flags and arguments:
    [-a <ACTION>] [-d <DATA_URI>] [-t <MIME_TYPE>]
    [-c <CATEGORY> [-c <CATEGORY>] ...]
    [-e|--es <EXTRA_KEY> <EXTRA_STRING_VALUE> ...]
    [--esn <EXTRA_KEY> ...]
    [--ez <EXTRA_KEY> <EXTRA_BOOLEAN_VALUE> ...]
    [--ei <EXTRA_KEY> <EXTRA_INT_VALUE> ...]
    [--el <EXTRA_KEY> <EXTRA_LONG_VALUE> ...]
    [--ef <EXTRA_KEY> <EXTRA_FLOAT_VALUE> ...]
    [--eu <EXTRA_KEY> <EXTRA_URI_VALUE> ...]
    [--ecn <EXTRA_KEY> <EXTRA_COMPONENT_NAME_VALUE>]
    [--eia <EXTRA_KEY> <EXTRA_INT_VALUE>[,<EXTRA_INT_VALUE...]]
        (mutiple extras passed as Integer[])
    [--eial <EXTRA_KEY> <EXTRA_INT_VALUE>[,<EXTRA_INT_VALUE...]]
        (mutiple extras passed as List<Integer>)
    [--ela <EXTRA_KEY> <EXTRA_LONG_VALUE>[,<EXTRA_LONG_VALUE...]]
        (mutiple extras passed as Long[])
    [--elal <EXTRA_KEY> <EXTRA_LONG_VALUE>[,<EXTRA_LONG_VALUE...]]
        (mutiple extras passed as List<Long>)
    [--efa <EXTRA_KEY> <EXTRA_FLOAT_VALUE>[,<EXTRA_FLOAT_VALUE...]]
        (mutiple extras passed as Float[])
    [--efal <EXTRA_KEY> <EXTRA_FLOAT_VALUE>[,<EXTRA_FLOAT_VALUE...]]
        (mutiple extras passed as List<Float>)
    [--esa <EXTRA_KEY> <EXTRA_STRING_VALUE>[,<EXTRA_STRING_VALUE...]]
        (mutiple extras passed as String[]; to embed a comma into a string,
         escape it using "\,")
    [--esal <EXTRA_KEY> <EXTRA_STRING_VALUE>[,<EXTRA_STRING_VALUE...]]
        (mutiple extras passed as List<String>; to embed a comma into a string,
         escape it using "\,")
    [--grant-read-uri-permission] [--grant-write-uri-permission]
    [--grant-persistable-uri-permission] [--grant-prefix-uri-permission]
    [--debug-log-resolution] [--exclude-stopped-packages]
    [--include-stopped-packages]
    [--activity-brought-to-front] [--activity-clear-top]
    [--activity-clear-when-task-reset] [--activity-exclude-from-recents]
    [--activity-launched-from-history] [--activity-multiple-task]
    [--activity-no-animation] [--activity-no-history]
    [--activity-no-user-action] [--activity-previous-is-top]
    [--activity-reorder-to-front] [--activity-reset-task-if-needed]
    [--activity-single-top] [--activity-clear-task]
    [--activity-task-on-home]
    [--receiver-registered-only] [--receiver-replace-pending]
    [--selector]
    [<URI> | <PACKAGE> | <COMPONENT>]
```
