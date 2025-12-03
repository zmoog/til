# Say out loud when a command completes

Sometimes you run a command that takes a long time to complete (e.g., a smoke test), and you want to be notified when it's finished so you can inspect the outcome.

On macOS you can use the `say` command:

```sh
$ make long-running-task && say the long-running task is done
```

When the `make long-running-task` exits, your Mac will say aloud "the long-running task is done." 
