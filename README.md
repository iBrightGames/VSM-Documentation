## VSM

Welcome to the VSM(Visual State Machine) documentation!<br/>
In this documentation, you can find how to use VSM in your project and how to customize it for your own purposes.

### What is VSM?

VSM is a State Machine visualizer that you can use for any purpose that works with state machines. For example, you can prepare a whole new dialogue system (which is an intended use) or a quest system that fully works with rewards and etc.

### VSM is WIP project
VSM is a Work In Progress project that will get updates over time. New nodes and systems will be implemented time to time. So if you don't know how to customize and doesn't want to learn how, you can check for our pre-build systems that will come with VSM. 

### License
You can customize this tool as much as you need if you bought it already, but you can't share or redistribute this for any purpose. Distributing rights for this tool is belong to iBright Games.

## Logic

### What is Logic
Logic is script that decides the behavioral activity of Graph. Different Logics means different graphs. This systems allows to use different systems on combination with each-other without rewriting all scripts at all. Different logics can use same nodes and systems at all.

There is a public static GetLogic(StateData) function in the StateGraphLogic.cs
This functions returns which logic should be used for each different StateData. Different State Data's may use same logic.

### How to Use Logics
Logics can be used to change behavioral activity of the Graph. Creating new logic and changing the GetLogic method for related StateData will change the activity of all graphs for that data type.

### How to Create Custom Logic
Creating new C# script inheriting StateGraphLogic will result a new logic. Placing this logic into GetLogic function will change the activity. 

1. Create a new C# script
2. Make sure using same libraries with StateGraphLogic.cs
3. Change Monobehaviour to StateGraphLogic
4. Add new Logic into StateGraphLogic.GetLogic(StateData) function's switch statement.
5. Customize your logic as you wish.


### How to Customize a Logic
Logics use some specific methods to change activities of graph. You can override these methods and write your own activities inside them. Methods and properties are listed below:

* **public override List<object> Nodes**<br/>
This should return the nodes that will be used in your logic. You should follow the following syntax:<br/>
`
public override List<object> Nodes => new List<object>
{
    new StateNode(),
    new CustomNode()
};
`

* **public override List<object> BlackboardProperties**<br/>
This should return the Blackboard Properties that will be used in your logic. You should follow the following syntax:<br/>
`        
public override List<object> BlackboardProperties => new List<object>()
{
    new BlackboardProperty(),
    new CustomProperty()
};
`

* You can implement new groups of nodes by duplicating Nodes return and overriding following SearchTreeEntries function.

* **public override List<SearchTreeEntry> SearchTreeEntries(Texture2D)**<br/>
This method overrides the popup menu that opens when creating new nodes. You should create a list of SearchTreeEntry in order and return that.<br/>
_Check DialogueGraphLogic.cs for more detail._

## Nodes
    
### How to Add Nodes

1. Create a new C# script that inherits from StateNodeData.cs.
2. Create a new C# script in Editor folder that inherits from StateNode.cs.

_Note: You can create add your custom type to NodeTypes by customizing NodeType.cs code. It's default location is:,<br/>_
`./DialogueSystem/Runtime/NodeUtilities/NodeType.cs`

_Check base scripts for override functions._

### How to Edit Nodes

1. Find related node's C# script.
2. If you want to edit the view of the node, you should go for Editor folder and [nodeName].cs
3. If you want to edit the data of the node, you should go for [nodeeName]Data.cs
4. You can edit these C# scripts as you wish.


### How to Implement Nodes on Logics
To use newly created nodes, you should implement them into related logics.<br/>
Find/Create your custom logic script and implement these nodes into SearchTreeEntries and OnSelectEntry methods. This will result you nodes to be shown on pop-up menu with related database.


### How to Create new Database
To use different logic, you need different databases. You can create custom databases easily.

1. Create C# script that inherits from StateData.cs
2. Voila! You now have custom database.
3. You can add your new nodes in your custom database List<newNode> and start using it.
    
## Dependencies

### Requirements

VSM(Visual State Machine) has some dependencies over Unity. 
These are listed below:

* Unity **Version: 2019.1** or **higher**
