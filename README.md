### sync-engine
---
https://github.com/nylas/sync-engine


```py
// tests/transactions/test_transaction_creation.py

from tests.util.base import (add_fake_message, add_fake_thread, add_fake_event,
  add_fake_category)
  
def get_latest_transaction(db_session, object_type, record_id, namespace_id):
  return db_session.query(Transaction).filter(
    Transaction.namespace_id == namespace_id,
    Transaction.object_type == object_type,
    Transaction.record_id == record_id). \
    order_by(desc(Transaction.id)).first()

```

```
```

```
```
