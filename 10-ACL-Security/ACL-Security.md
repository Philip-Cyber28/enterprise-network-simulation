# ACL Security

## 1. Objective
Control network traffic between selected networks using standard and/or extended access control lists.

## 2. Security Requirements
Document the actual traffic rules implemented. For example:
- Which VLANs are allowed to access server services?
- Is guest access restricted from internal department networks?
- Which devices are allowed to manage network equipment?

## 3. ACL Policy
| ACL name/number | Applied on device/interface | Direction | Purpose |
|---|---|---|---|
| [ACL] | [Interface] | [In/Out] | [Traffic rule] |

## 4. Configuration
Insert the actual ACL commands used.

Example syntax:

```cisco
access-list [NUMBER] permit [SOURCE] [WILDCARD-MASK]
access-list [NUMBER] deny [SOURCE] [WILDCARD-MASK]
```

For extended ACLs, document the source, destination, protocol, and permitted or denied service.

## 5. Verification
```cisco
show access-lists
show ip interface
```

## 6. Testing Results
Test both permitted and denied traffic. Record the source, destination, expected result, and actual result.

## 7. Screenshots
Add ACL configuration and successful/blocked traffic test screenshots.
