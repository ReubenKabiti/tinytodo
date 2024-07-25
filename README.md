# Building and running

To build this project make sure you have the latest version of rust installed [rustup](https://www.rust-lang.org/tools/install).
In the project root run 
``` sh
cargo build
```
To run the application, run
``` sh
python -i ./tinytodo.py
```

To run the tests, run
``` sh
python -m unittest test_tinytodo.py
```
To start the server, from the Python primary prompt `>>>` enter

```python
start_server()
```

When it starts up, the server reads in the Cedar policies in `policies.cedar`, and the Cedar entities, which define the TinyTodo `User`s and `Team`s, from `entities.json`. It validates the policies are consistent with `tinytodo.cedarschema`, and will abort if they are not.

Client code `tinytodo.py` defines the functions you can call, which serve as the list of commands. See also [`TUTORIAL.md`](./TUTORIAL.md) for a detailed description of how to use these commands, and how TinyTodo works. Here is a brief description of the commands:

* `start_server()` -- starts the TinyTodo server on port 8080. To use port XXX instead, provide `port=XXX` as the argument instead. Fails if server is already running.
* `stop_server()` -- shuts down the TinyTodo server, if running. Called automatically on exit.
* `set_user(user)` -- sets the user to use for the commands that follow. Parameter `user` can be any of `emina`, `aaron`, `andrew`, or `kesha`. In the following commands, you can override this user by providing an additional parameter at the start that names the user.
* `get_lists()` -- gives the lists owned by the current user
* `create_list(name)` -- creates the list named `name` (a string) owned by the current user; prints the numeric ID of the created list on success
* `get_list(list)` -- gets information about list `list`, indicated by its numeric ID.
* `create_task(list,name)` -- creates a new (uncompleted) task for list `list` named `name` (a string); prints the task's numeric ID on success, which is its position in the list
* `toggle_task(list,task)` -- toggles the completion status of the task `task` (a numeric ID) for list `list`
* `change_task_description(list,task,name)` -- changes the name of task `task` in list `list` to `name` (a string)
* `delete_task(list,task)` -- deletes task `task` from list `list`. Reorders remaining tasks
* `delete_list(list)` -- deletes the given list
* `share_list(list,target,readonly)` -- shares the given list with `target`; if `readonly` (a boolean) is `True` then the target has _reader_ status for the list, else _editor_ status. `readonly` is an optional parameter, defaulting to readonly. `target` can be a user or a team, where legal teams are `temp`, `interns`, and `admin`
* `unshare_list(list,target)` -- revokes access to `list` for `target`, which can be a user or a team
