# Role Based Access Control (RBAC)

High-level view of Owl’s Security architecture depicted below.

![](https://lh3.googleusercontent.com/Fw3N1MBaOdHcOrXlOGr9sYn4RGbnakMorQjeLnEJcoihKhaJaZ-H4OtxiXo6b6B6O404EfgpXhegs6OJtUJkurjwJVwSa-haXkPAY5W7tvV0QTN3Y4Zk2qQDZkAn3WWoE2v2S\_ig)

Whether leveraging a Local User Store, Active Directory, or using the out of the box user accounts that come with Owl via LDIF, security stays the same. An admin can create many ROLE’s. A user, whether local user, LDIF user, or AD user can be part of one or many roles. And a ROLE maps to a Dataset within Owl.

A unique feature within Owl is the fact that Owl does not store information about external user accounts. This avoids the need to sync external users from an external user store such as AD to owl. Instead Owl will map the external group to an internal role. From here the ROLE can be mapped to the different functionality within Owl whether they are Admins / Users / and have access to different datasets and future functionality. The other benefit is that if a specific userid within the external user store is terminated, when the user is purged from the external user store such as AD they will immediately not have access to Owl’s web application. This is because when the user logs into Owl’s web application that is backed by AD their login will interrogate AD to authenticate the user account. See logical flow below for how the group to role mappings work.

![](https://lh5.googleusercontent.com/6lYry5CMj2FBQC8mvyrG\_30FvI573q3\_NMm11DHL05UC-5SgH5NRUydAm9qNa-CihLCgA\_e4\_-NEUOqJfgGQgmioIO6QXOhkH8p4s4rACl6EkV7m1tg1ICNlij077p2mBc6qgPKd)

### RBAC Usages <a href="hrbacusages" id="hrbacusages"></a>

Owl supports RBAC configuration with both core roles and custom roles. Core roles include the following:

| Role                         | Access Description                                                                |
| ---------------------------- | --------------------------------------------------------------------------------- |
| ROLE ADMIN                   | Modify any access, config settings, connections, role delegation                  |
| ROLE DATA GOVERNANCE MANAGER | Ability to manage (create / update / delete) Business Units and Data Concepts     |
| ROLE USER MANAGER            | Create / modify users, add users to roles                                         |
| ROLE OWL ROLE MANAGER        | Create roles, edit role mappings to users / AD groups / datasets                  |
| ROLE DATASET MANAGER         | Create / modify datasets to roles, masking of dataset columns                     |
| ROLE OWL CHECK               | Only role that can run DQ scans if Owlcheck security is enabled                   |
| ROLE DATA PREVIEW            | Only role that can view source data if data preview security is enabled           |
| ROLE DATASET TRAIN           | Only role that can train datasets if dataset train security is enabled            |
| ROLE DATASET RULES           | Only role that can add / edit / delete rules if dataset rules security is enabled |
| ROLE PUBLIC                  | Public: Access to scorecards, no dataset access when dataset security is enabled  |

Custom roles can be added via the Role Management page by navigating to the Admin Console and clicking on the Roles Icon. Custom roles can also be added 'on the fly' during the Active Directory Role Mapping step.

It is these custom roles that will determine the users that have access to datasets (including profile/rules/data preview/scoring), and database connections

Additional information regarding setting up Dataset and Connection security can be found in those documents respectively.
