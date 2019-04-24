# Admin

\[TBD\]

As a system admin, I want to...

* Perform system bootstrap during setup/install, consolidated in a single service call
* Platform-wide auth, especially if a mediator is used for providing actual identity
* Create new tennant
* Delete tennant
* Add file\(s\) by URL
* Handle service deployment \(for new platform installations\)
* Perform system reset
  * Need to protect against accidental resets
  * Avoid restarting services after resetting the platform
* Ability to add new user\(s\)
* Ability to manage user permissions. Initially planning 3 modes:
  * All - tenant 0
  * RO
  * RW
* Ability to initiate/manage system back-up config, frequency, schedule, etc.
* Ability to monitor overall system performance/health
  * including service/container level
* Ability to scale services \(up or down\)
* Jobs page/section to show status of background tasks

