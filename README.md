# Script-Controlled ACL – Restrict Record Access Based on Custom Script

Naan Mudhalvan - ServiceNow System Administrator project

## About
A Script-Controlled ACL restricts access to records using a custom script. The script checks field values and user
conditions before granting access, and users can access the record only when the ACL script evaluates to **true**.

## Team
| Name | Role |
|------|------|
| Shanmugapriya B | Team Lead - Project planning, architecture and ACL scripting |
| Shrivinoj Karthikeyan | Member - Tables creation and READ / CREATE ACLs |
| Mohammed Ameen S | Member - WRITE / DELETE ACLs and testing |
| Srinithi T | Member - Users and roles setup, documentation |

Team ID: SWTID-2026-9494

## Milestones
1. Creation of Users and Roles
2. Tables Creation
3. Access Control List - READ
4. Access Control List - CREATE
5. Access Control List - WRITE
6. Access Control List - DELETE
7. Conclusion

## Repository structure
```
1. Ideation Phase/
2. Requirement Analysis/
3. Project Design Phase/
4. Project Planning Phase/
5. Project Development Phase/
6. Project Documentation/
```

## Links
- Demo video: [add link]
- GitHub: [add link]

## ACL scripts
### Read
```javascript
answer = false;
if (gs.hasRole('u_record_admin')) {
    answer = true;                       // admins can read every record
} else if (current.u_owner == gs.getUserID()) {
    answer = true;                       // owners can read their own records
} else if (gs.hasRole('u_record_user') && current.u_confidential == false) {
    answer = true;                       // users can read non-confidential records
}
```
### Create
```javascript
answer = gs.hasRole('u_record_admin') || gs.hasRole('u_record_user');
```
### Write
```javascript
answer = false;
if (gs.hasRole('u_record_admin')) {
    answer = true;
} else if (current.u_owner == gs.getUserID() && current.u_status != 'closed') {
    answer = true;                       // owner may edit until the record is closed
}
```
### Delete
```javascript
answer = gs.hasRole('u_record_admin');
```
