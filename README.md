# todo_app
## CRUD

CRUD applications are fundamental in software development, representing the four basic operations: Create, Read, Update, and Delete. These operations allow users to interact with databases and manage data effectively.

| Operation | SQL Command | SQLAlchemy Command |
|-----------|-------------|--------------------|
| Create    | INSERT      | `db.session.add(user)`    |
| Read      | SELECT      | `user.session.query()`  |
| Update    | UPDATE      | `user.foo = "new value"`  |
| Delete    | DELETE      | `db.session.delete()` |

### SQLAlchemy ORM Instructions

1. **Setup SQLAlchemy:**
  ```python
  from sqlalchemy import create_engine
  from sqlalchemy.ext.declarative import declarative_base
  from sqlalchemy.orm import sessionmaker

  engine = create_engine('sqlite:///example.db')
  Base = declarative_base()
  Session = sessionmaker(bind=engine)
  session = Session()
  ```

2. **Define a Model:**
  ```python
  from sqlalchemy import Column, Integer, String

  class User(Base):
     __tablename__ = 'users'
     id = Column(Integer, primary_key=True)
     name = Column(String)
     age = Column(Integer)
  ```

3. **Create the Table:**
  ```python
  Base.metadata.create_all(engine)
  ```

4. **Create (INSERT):**
  ```python
  new_user = User(name='John Doe', age=30)
  session.add(new_user)
  session.commit()
  ```

5. **Read (SELECT):**
  ```python
  users = session.query(User).all()
  for user in users:
     print(user.name, user.age)
  ```

6. **Update (UPDATE):**
  ```python
  user = session.query(User).filter_by(name='John Doe').first()
  user.age = 31
  session.commit()
  ```

7. **Delete (DELETE):**
  ```python
  user = session.query(User).filter_by(name='John Doe').first()
  session.delete(user)
  session.commit()
  ```