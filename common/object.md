# Object

All system managed objects generally have the following attributes and actions.

TODO: clarify other criteria - spaces, acceptable characters, etc.

### Attributes

- **Id**

  [*String, Required*] Id is system generated string, immutable and uniquely identifying an object. System must ensure its uniqueness within given workspace over the lifetime of the worksapce. Usually [UUIDs (GUIDs)](https://en.wikipedia.org/wiki/Universally_unique_identifier) are used for this.

  Example: 123e4567-e89b-12d3-a456-426655440000

  Max length: 40 characters

  Note: 40 characters is sufficient to represent either UUID or SHA-1 hashes as human readable strings.

- **Name**

  [*String, Required*]

  Name is string assigned by user, uniquely identifying an object. It's mutable, and can be changed by user as long as it stays unique within specific scope at any moment of time among non-archived objects. Scope is usually workspace, but in some cases uniqueness can be enforced within smaller scope, such as artifact names are unique only within run.

  Max length 255 characters.

  - **Status**

  [*Enum, Required*]

  Allowed values: Active, Deprecated, Archived

  Not all statuses are applicable to some object types.

  - *Active* object is visible in default lists, can be retrieved by name or id, and can be used in the system
  - *Deprecated* object is not visible in default lists, can be retrieved by name or id, and can be used in the system. User might be warned that this object is deprecated and recommended to use some other object instead.
  - *Archived* object is not visible in default lists, can't be retrieved by name and can't be used to execute new jobs. It can be retrieved by Id, most of metadata is still readable for the purpose of exploring history of past executions.

- **Description**

  [*String, Optional*].

  Arbitrary text description for given object.

  Max length 32K characters. 



### Actions

- Create

- Get

- Archive

  Object is not deleted. Name is can be reused for some other object.

- Rename



## Deletion

Hard deletion is unsupported for system managed objects. Objects can be archived to free up name, and hide object from default lists or UX. However, objects are preserved to allow user later discover history of ML, and prevent breakage of other objects referencing given object