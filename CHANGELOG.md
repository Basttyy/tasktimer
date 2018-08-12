# `TaskTimer` Changelog

All notable changes to this project will be documented in this file. The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/) and this project adheres to [Semantic Versioning](http://semver.org).

## 2.0.0 (2018-08-12) [UNRELEASED]
This release includes various **breaking changes**. Please see the [API reference][docs]. Also note that this version is completely re-written in TypeScript.

### Changed
- **Breaking**: `TaskTimer` is no longer a default export. See _Usage_ section in readme.
- **Breaking**: `TaskTimer#addTask()` renamed to `TaskTimer#add()`. This no longer accepts a `string` argument. It should either be an options object, a `Task` instance or a callback function. It also accepts an array of these, to add multiple tasks at once.
- **Breaking**: The task name is optional (auto-generated when omitted) when task is created via `#add()`. But `callback` is now required.
- **Breaking**: `TaskTimer#removeTask()` renamed to `TaskTimer#remove()`.
- **Breaking**: `TaskTimer#getTask()` renamed to `TaskTimer#get()`.
- **Breaking**: `TaskTimer.Event` enumeration is renamed to `TaskTimer.EventType`.
- **Breaking**: `TaskTimer.State` enumeration type is changed to `string`. (meaning enum values are also changed.)

### Added
- Task option: `enabled: boolean` indicating whether the task is currently enabled. This essentially gives you a manual control over execution. The task will always bypass the callback while this is set to `false`.
- Task option: `tickDelay: number` to specify a number of ticks to allow before running the task for the first time.
- Event: `TaskTimer.EventType.TASK_COMPLETED` (`"taskCompleted"`) Emitted when a task has completed all of its executions (runs) or reached its stopping date/time (if set). Note that this event will only be fired if the tasks has a `totalRuns` limit or a `stopDate` value set.
- Event: `TaskTimer.EventType.COMPLETED` (`"completed"`) Emitted when *all* tasks have completed all of their executions (runs) or reached their stopping date/time (if set). Note that this event will only be fired if *each* task either have a `totalRuns` limit or a `stopDate` value set, or both.
- Timer option: `stopOnCompleted: boolean` indicating whether to automatically stop the timer when all tasks are completed. For this to take affect, all added tasks should have `totalRuns` and/or `stopDate` configured. Default: `false`
- Timer property: `runCount: boolean` indicating the total number of all task executions (runs).
- TypeScript support.

### Fixed
- An issue where default task options would not be set in some cases. Fixes issue [#5](https://github.com/onury/tasktimer/issues/5).

### Removed
- **Breaking**: `TaskTimer#resetTask()` is removed. Use `#get(name).reset()` to reset a task.
- Dropped bower support. Please use npm to install.
- (Dev) Removed grunt in favour of npm scripts. Using jest instead of jasmine-core for tests.


## 1.0.0 (2016-08-16)

- Initial release.


[docs]:https://onury.io/tasktimer/?api=tasktimer