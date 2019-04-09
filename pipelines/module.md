# Modules

Module represents a unit of computation, defining script which will run on compute target, and describing its interface. Module  interface describes inputs, outputs, parameter definitions, but doesn't bind them to specific values or data. Module has snapshot associated with it, capturing script, binaries and other files necessary to execute on compute target. 

Module is container of ModuleVersions. Users can publish new versions, deprecate them, and otherwise manage.

## Publishing new module version

There are multiple ways to publish new ModuleVersion:

- Using UX, CLI, SDK, REST
- Snapshot can originate from many sources: git commit, folder, vsts artifact, existing snapshot, docker image

Publishing is in a scope of workspace. 

## Consuming module

In most cases users will reference/consume Module, not ModuleVersion. System will be responsible for resolving Module->ModuleVersion in meaningful time:

- When publishing pipeline, if user used Module in their graph, we should preserve Module reference and resolve ModuleVersion only during submission

  - Challenge here is that interface is defined for ModuleVersion, not Module. So we can offer interface checks with authoring graph, but can't enforce them - actual module version might have different interface so interface enforcement can only happen when pipeline run is triggered

- When submitting pipeline for execution, Module is resolved to ModuleVersion immediately when submitting graph

- User can always use ModuleVersion in either of above scenarios, and we don't need to perform any binding.

Generally if user doesn't care about versioning too much, they just publish and consume Module, and always work with latest. Underlying infra tracks actual executed instances as ModuleVersion and user can always fall back to binding specific version.

## Mutability

Module has mutable and immutable metadata. Most of metadata is mutable.

Mutable: name, description, versions, status

Immutable: id, creation time



ModuleVersion has mutable and immutable metadata. Most of metadata is immutable.

Immutable: id, snapshot id, inputs, outputs, parameters, creation time, status etc. Generally any fields influencing execution are immutable.

Mutable: description

## Naming and identifiers

Module has name assigned by user, which must be unique within workspace. Module ID is system generated unique identifier. Module name can be changed by user (renaming modules), and is also "freed up" from user space when module is archived. Module Id is unique and immutable.


## Entities

 - Module

   ```json
   {
       "id": "266c582a-a92b-478f-93b3-66a89b755bbf",
       "name" : "My training module",
       "description" : "I dreamed epic algo and coded a new boosted decision trees algo, just need to make it work now",
       "status" : "active",
       "createdUtc" : "2019/01/01 12:12:32Z",
       "versions" : [
       	{
               "version" : "1",
               "id" : "b27ce40e-4ddd-4ef5-8f7b-095621f29a03"
           },
           {
               "version" : "2",
               "id": "db47be6b-8e73-403c-9280-0e30a8dc80d3"
           }
       ]
   }
   ```

   

 - ModuleVersion

   ```json
   {
   
   	"id" : "b27ce40e-4ddd-4ef5-8f7b-095621f29a03",
   	"module" : "266c582a-a92b-478f-93b3-66a89b755bbf",
    "description" : "final attempt3",
    "version" : "1",
    "status" : "deprecated",
    "snapshot_id" : "blah",
    "createdUtc" : "2019/01/01 12:12:32Z",
    "inputs": TBD,
    "outputs" : TBD,
    "params" : TBD    
   
   }
   ```

   