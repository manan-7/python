##3 File Context example

```
class FileManager:
  def __init__(self, filename):
    self.filename = filename
    self.file = None

  def __enter__(self):
    self.file = open(self.filename, 'w')
    return self.file  # Return the opened file for writing

  def __exit__(self, exc_type, exc_val, exc_tb):
        # to teardown resource
        # self: The context manager object itself.
        # exc_type: The type of exception raised within the with block (None if no exception).
        # exc_val: The exception object itself (None if no exception).
        # exc_tb: The traceback object (None if no exception).
    if self.file:
      self.file.close()  # Close the file on exit

# Use the context manager with the 'with' statement
with FileManager('data.txt') as f:
  f.write('This is some data!')  # Use the returned file object 'f'

# Here, the file is automatically closed after the 'with' block exits

  ```
