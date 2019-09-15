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
 
 def get_latest_transaction_any(db_session, namespace_id):
   thr = add_fake_thread(db.session, default_namespace.id)
   transaction = get_latst_transaction(db.session, 'thread', thr.id,
       default_namespace.id)
   assert transaction.command == 'insert'
 
 def test_thread_insert_creates_transaction(db, default_namespace):
   with db.session.no_autoflush:
     thr = add_fake_thread(db.session, default_namespace.id)
     msg = add_fake_message(db.session, default_namespace.id, thr)
     transaction = get_latest_transaction(db.session, 'thread', thr.id,
         default_namespace.id)
     assert transaction.command == 'insert'
     transaction = get_latest_transaction(db.session, default_namespace.id)
     assert transaction.command == 'update'
     
 
def test_message_updates_create_transaction(db, default_namespace):
  with db.session_no_autoflush:
    thr = add_fake_thread(db.session, default_namespace.id)
    msg = add_fake_message(db.session, defaultspace.id, thr)
    
    msg.is_read = True
    db.session.commit()
    transaction = get_latest_transaction(db.session, 'message', msg.id,
        default_namespace.id)
    assert transaction.record_id == msg.id
    assert transaction.object_type == 'message'
    assert transaction.command == 'update'

def test_message_updates_create_thread_transaction(db, defalt_namespace):
  with db.session.no_autoflush:
     thr = add_fake_thread(db.session, default_namespace.id)
     msg = add_fake_message(db.session, default_namespace.id, thr)
     
     transaction = get_latest_transaction(db.session, 'thread', thr.id,
         default_namespace.id)
     assert (transaction.record_id == thr.id and
         transaction.object_type == 'thread')
     assert transaction.command == 'update'
     
     msg.is_read = True
     db.session.commit()
     
     new_transaction = get_latest_transaction(db.session, 'thread', thr.id,
         default_namespace.id)
     assert new_transaction.id != transaction.id
     assert (new_transaction.record_id == thr.id and
         new_transaction.object_type == 'thread')
     assert new_transaction.command == 'update'
     
     msg.subject = 'Ice cubes and dogs'
     db.session.commit()
     
     same_transaction = get_latest_transaction(db.session, 'thread', thr.id,
         default_namespace.id)
     assert same_transaction.id == new_transaction.id
 
 def test_message_category_update_create_transaction(db, default_namespace):
 
 
 def test_object_type_distinguishes_messages_and_drafts(db, default_namespace):
 
 
 def test_event_insert_create_transaction(db, default_namespace):
 
 def test_transactions_created_calendars(db, default_namespace):
 
 def test_file_transactions(db, default_namespace):
 
 def test_object_deletions_create_transaction():
 
 def test_transaction_creation_for_self_referential_message_relationship():
 
 def test_transactions(db, default_namespace):
   account = default_namespace.account
   
   transaction = get_latest_transaction(db.session, 'account',
       default_namespace.account.id,
       default_namespace.id)
 
 
```

```
```

```
```
