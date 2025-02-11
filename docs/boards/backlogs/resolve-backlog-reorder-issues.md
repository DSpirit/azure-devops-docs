---
title: Resolve nest, display, and reorder issues for work items
titleSuffix: Azure Boards
description: Learn how to fix reordering and nesting issues for work items in Azure Boards. Resolve error messages and maintain a natural hierarchy for your backlog.
ms.custom: boards-backlogs
ms.service: azure-devops-boards
ms.assetid: BDEAA5D4-83A3-49FC-BEEB-EE685E92B68B
ms.topic: troubleshooting
ms.author: chcomley
author: chcomley
monikerRange: '<= azure-devops'
ms.date: 10/17/2023
---

# Fix reordering and nesting issues

<a id="display-hierarchy">  </a>

[!INCLUDE [version-lt-eq-azure-devops](../../includes/version-lt-eq-azure-devops.md)]
<!--- Supports FWLINK https://go.microsoft.com/fwlink/?linkid=529135 --> 

When you reorder, nest, and display work items, Azure DevOps expects a [natural hierarchy](#natural-hierarchy-for-work-item-types). The natural hierarchy breaks when you create same-category or same-type links between work items. For example, parent to child links that are bug to bug or user story to user story or *requirements* category to *task* category. Use this article to address error messages when you add links that aren't in the natural hierarchy.

## "You cannot reorder work items and some work items might not be shown"

You might see an error similar to one of the following messages:

> - You cannot reorder work items and some work items might not be shown
> - No work item IDs are listed 

To address this error, do the following steps: 

1. Open your backlog.
2. Review the list of items to identify those of the same type that are nested.  
   
   - **Example #1:** The following image shows a user story as a child of another user story. 

   :::image type="content" source="media/resolve/nested-user-stories.png" alt-text="Screenshot showing nested user stories on a backlog.":::
	
   - **Example #2:** The following image shows a bug as a child of a user story. When the backlog displays user stories and bugs at the same level (Requirements category), it results in a nested item that disables the ordering feature.

   :::image type="content" source="media/resolve/nested-user-story-bug.png" alt-text="Screenshot of nested user story and bug.":::
	
3. Remove any parent-child links that exist among nested items of the same work item type or category, or consider changing the link type to 'Related.'
4. Refresh your backlog.

Following these steps should resolve the issue, and the error message no longer displays.

## "Work item can't be reordered because its parent is on the same category"

You might see an error similar to one of the following messages: 

> - You cannot reorder work items and some work items might not be shown. See work item(s) 7 to either remove the parent to child link or change the link type to Related.
> - Work item 3 can't be reordered because its parent is on the same category. 

To address this error, do the following steps: 

1. Open the work item listed in the error message.
2. Look for a parent or child link. Make sure this link goes to a work item within the same category as the work item you opened. This link goes to another work item  that appears on the same backlog level as the work item you opened. Depending on your team's bug behavior setting, bugs might appear with requirements or tasks. 
3. Remove the problem parent-child link. If you would like to keep these items associated, use 'Related' link type instead. 

The message no longer displays.

## "Work items in progress might disappear on refresh"

You might see an error similar to one of the following messages: 

> Items added to the backlog might disappear on a refresh because your team project marks them as "in progress". Those items appear when you change the "In progress" filter to Show. 

This message indicates that the **In Progress** filter for the backlog is turned off.  

When you refresh your browser, the work items display based on your selected filters. To reset the filters, do the following steps. 

::: moniker range=">= azure-devops-2019"
1. Open your backlog.
2. From the **View options** selector, choose to show or hide **In Progress items**. 

- If you turn the **In Progress** control off, then items that are in the *Active*, *Committed*, or *Resolved* states or states that map to the [**In Progress** category state](../work-items/workflow-and-state-categories.md) don't appear.
  
::: moniker-end

::: moniker range=">= azure-devops-2020" 

   :::image type="content" source="media/create-backlog/in-progress-control-2020.png" alt-text="Screenshot of View options selector, In progress control, version 2020 and later.":::
   
::: moniker-end
::: moniker range="azure-devops-2019"
   :::image type="content" source="media/create-backlog/in-progress-control-2019.png" alt-text="Screenshot of View options selector, In progress control, version 2019.":::
::: moniker-end
::: moniker range="tfs-2018"
1. Open your backlog.
2. Show or hide **In progress items** on your backlog. 
   - If you turn the **In Progress items** control off, then items that are in the *Active*, *Committed*, or *Resolved* states or states that map to the [**In Progress** category state](../work-items/workflow-and-state-categories.md) don't appear. 

::: moniker-end
 - Hide **In Progress items** when you want to forecast work. For more information, see [Forecast your product backlog](../sprints/forecast.md).

> [!NOTE]   
> - For more information, see [Configure your backlog view](configure-your-backlog-view.md) and [Add custom work item types](../../organizations/settings/work/add-custom-wit.md).
> - For issues that might occur with multi-team ownership, see [Configure a hierarchy of teams, Exercise select features with shared area paths](../plans/configure-hierarchical-teams.md#op-issues).
> - To reorder work items on your backlog, you must have Basic or higher level access. If you have Stakeholder access, you can't reorder work items. For more information, see [Stakeholder access quick reference](../../organizations/security/stakeholder-access.md).

## Natural hierarchy for work item types

The following image shows the natural hierarchy for the Agile, Scrum, and Capability Maturity Model Integration (CMMI) processes.

:::image type="content" source="media/resolve/create-hierarchy-with-different-wits.png" alt-text="Conceptual image of natural hierarchy for the Agile, Scrum, and CMMI processes.":::

## Best practices

**Do:** 
- Maintain a flat list, rather than nesting requirements, bugs, and tasks. 
- Only create parent-child links one level deep between items that belong to a different category. The category a work item belongs to gets determined by your process levels and your team's selected bug behavior.
- Use the *feature* work item type to group user stories (Agile), issues (Basic), work items (Scrum), or requirements (CMMI). You can [quickly map work items to features](organize-backlog.md), which creates parent-child links in the background.

**Don't:**
- Create a hierarchy of work items, tasks, and bugs. 
- Establish same-category hierarchies, such as parent-child links among work items of the same type (for example, story-story, bug-bug, task-task, or issue-issue). The backlog, board, and sprints experiences don't support reordering for same-category hierarchies, as it introduces confusion by ordering a work item that doesn't belong at that level.

## Track bugs as requirements or tasks  

[Each team has the flexibility to choose how to track bugs](../../organizations/settings/show-bugs-on-backlog.md)—whether as requirements, tasks, or neither. See the following guidelines: 

- **If you track bugs as *requirements***: Nest them only under the *Feature* level.

   :::image type="content" source="media/resolve/bugs-as-requirements.png" alt-text="Screenshot of linked bugs like requirements."::: 

- **If you track bugs as *tasks***: Nest them only under the *Requirement* level.

   :::image type="content" source="media/resolve/bugs-as-tasks.png" alt-text="Screenshot of linked bugs like tasks, underneath the Requirement level.":::

## Display nested items on backlogs and boards

Sprint backlogs and Taskboards exclusively display the last node in a same-category hierarchy, which is referred to as the leaf node. 

::: moniker range="tfs-2018"
> [!NOTE]
> - For TFS 2018 and earlier versions, the Kanban board only shows the last node with nested items of a same-category hierarchy.
> - For TFS 2018.2 and later versions, Kanban boards display all work items of nested same-category work items.  
::: moniker-end

::: moniker range="tfs-2018"

### Product backlog and Kanban boards

If you link items within a same-category hierarchy that is **four levels deep**, for instance, **only the items at the fourth level** appear on the Kanban board, sprint backlog, and Taskboard.

As shown in the following images, the third user story, *Interim save on long form*, has a child bug named *Save takes too long*. While the child bug, *Save takes too long*, appears on the Kanban board, the parent user story doesn't.  

**All bugs and requirements appear on the backlog**  

:::image type="content" source="media/resolve/bugs-appear-on-backlog.png" alt-text="Screenshot showing child bug on backlog.":::

**Only leaf nodes appear on the Kanban board**  

:::image type="content" source="media/resolve/bugs-appear-on-board.png" alt-text="Screenshot showing leaf node bug on Kanban board.":::

::: moniker-end

### Sprint backlogs and Taskboards

When tasks and bugs link to their parent requirements, they group them correctly on the sprint backlog and Taskboard. 
But, when you establish parent-child links between a requirement and a bug, and between the bug and a task, as demonstrated here, the task appears on the sprint backlog and Taskboard, while the bug doesn't.

**Hierarchy of items assigned to a sprint backlog**  

:::image type="content" source="media/resolve/sprint-backlog-hierarchy.png" alt-text="Screenshot of Sprint backlog query with linked bug and task.":::  

**Only leaf nodes appear on sprint backlogs**  

:::image type="content" source="media/resolve/sprint-backlog-leaf-only.png" alt-text="Screenshot of Sprint backlog with leaf node task."::: 

**Only leaf nodes appear on Taskboards**

:::image type="content" source="media/resolve/bugs-appear-on-taskboard.png" alt-text="Screenshot of Sprint board with leaf node task.":::

## Frequently asked questions (FAQs)

### Q: Is there a workaround to display intermediate nodes within a hierarchy?  
A: No, not at this time. You can always check the entire list of items assigned to a sprint when you select **Create query**. 

## Related articles

- [Set up your backlogs and boards](set-up-your-backlog.md)  
- [About boards and Kanban, Limitations of multi-team Kanban board views](../boards/kanban-overview.md)  
