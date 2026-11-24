# Changelog
## 3.0.0
Fork of `diablomedia/zendframework1-session-savehandler-dbtable`, published as `gizmocraft/zendframework1-session-savehandler-dbtable`.
### Breaking changes
- Requires PHP `>=8.5`. Tested on PHP 8.5 and 8.6.
- Package renamed from `diablomedia/zendframework1-session-savehandler-dbtable` to `gizmocraft/zendframework1-session-savehandler-dbtable`. It now requires `gizmocraft/zendframework1-config` `^3.0.0`, `gizmocraft/zendframework1-session` `^3.0.0` and `gizmocraft/zendframework1-db` `^2.0.0`.
### Other changes
- PHP 8.6: `session_set_save_handler()` deprecates handler objects without `create_sid()` and `validateId()` (required in PHP 9.0). `Zend_Session_SaveHandler_DbTable` now also implements `SessionIdInterface` and `SessionUpdateTimestampHandlerInterface`. New public methods: `create_sid(): string` (random hex id honouring `session.sid_length`), `validateId($id): bool` (true for an existing, non-expired session; used by `session.use_strict_mode`) and `updateTimestamp($id, $data): bool` (delegates to `write()`; used by `session.lazy_write`). Existing signatures are unchanged.
- Dev dependencies upgraded (PHPUnit 13, PHPStan 2.3, php-cs-fixer 3.95, GrumPHP 2.27). Dropped `composer-require-checker`, which has no release for PHP 8.6.
- Tests migrated to PHPUnit 13 attributes, with tests for the new methods. `testReadWriteTwiceAndExpire` asserts the empty string returned for an expired session instead of calling `unserialize('')`, which warns.
- Removed an obsolete PHPStan ignore.
- CI runs PHP 8.5 and 8.6.
