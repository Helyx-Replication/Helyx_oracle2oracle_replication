# Security & Privilege Justification

This section explains the security model followed by Helyx and provides a clear justification for every database privilege granted. This section is intended for security teams, auditors, and compliance reviewers.

### Source Database Security Model
Helyx operates in a non-intrusive, read-only capture mode on the source database. It does not alter application data or schemas. Privileges granted are strictly limited to what is required for redo log mining and internal metadata handling.

### Source Database Privileges – Justification
__CONNECT__
+ Required to establish authenticated sessions.

__RESOURCE__
+ Required for managing internal control tables such as the Debezium signal table.

__UNLIMITED TABLESPACE__
+ Prevents replication interruptions caused by space exhaustion.
