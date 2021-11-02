---
description: Quickly click on items to trigger re-training
---

# Item Labeling

{% hint style="warning" %}
Note: There are limitations with item labeling.  Not all line items are eligible for all labeling options (Validate, Invalidate, Resolve).  Please see the breakdown below on which options are available per DQ detection tab. Some of this is by design.  Additionally, we are normalizing the actions and updating documentation for clarity.
{% endhint %}

![](../.gitbook/assets/item\_label.gif)

## Re-train the Owl DQ Model

By clicking the down arrow, you are telling Owl that this finding is not an actual DQ item. Another way to say it is "I don't want to be alerted to this item in the future". Owl allows a user to annotate the reasoning while keeping an audit log of the event. You can bring the item back into play by navigating to the "Labels" panel and deleting the down trained item. Owl will prompt a user to re-train the model after clicking a down arrow.

```
Behaviors - Validate, Resolve (You cannot invalidate something that is generated)
Rules - NONE (Managed through Rules Interface)
Outliers - Validate, Invalidate, Resolve
Pattern - Validate, Invalidate, Resolve
Source - Validate, Invalidate, Resolve
Record - Validate, Resolve 
Schema - Validate, Resolve 
Dupes - Invalidate Only 
Shapes - Validate, Invalidate, Resolve
```

Users can assign items or label for future runs.

![Each item will have an action to assign or dismiss the item.](<../.gitbook/assets/image (102).png>)

![](<../.gitbook/assets/image (97).png>)
