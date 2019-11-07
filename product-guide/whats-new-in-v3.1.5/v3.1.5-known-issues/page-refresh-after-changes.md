---
description: Must refresh page to apply changes after removing.
---

# RC2-002: Page Refresh After Changes

{% tabs %}
{% tab title="Description" %}
Refreshing the page everything is fine.
{% endtab %}

{% tab title="Repro Steps" %}
1. Create kind1 with any fields.
2. Create kind2 with field of the type kind1.
3. Create function with any in/out fields\(needs to have empty CKG errors\).
4. Execute query CKGErrors and make sure there is no errors.
5. Remove kind1 using delete button.
{% endtab %}

{% tab title="Expected Result" %}
Kind removed everywhere \(Explorer, Inventory, fields type\).  
CKGErrors doesn't return errors.
{% endtab %}

{% tab title="Actual Result" %}
Kind removed from the inventory and explorer, but can see reference to the removed kind in the kind2 and CKGErrors shows error:

```python
{
  "data": {
    "CKGErrors": [
      "Error while introspecting KindDB Model schema: [{\"message\":\"Error: Failed to find type for field: { id: 'a52225e5-3907-4c36-a055-eee982947d0f',\\n  name: 'k1',\\n  description: '',\\n  type: 'KIND',\\n  typeKindId: '1b2a3079-47d7-4ae1-99e8-993f93661b76',\\n  modifiers: [],\\n  kind: null,\\n  hide: false,\\n  autoFocus: false,\\n  displayAs: [],\\n  readonly: false,\\n  isDeleted: false }\"}]"
    ]
  }
} 
```
{% endtab %}
{% endtabs %}

