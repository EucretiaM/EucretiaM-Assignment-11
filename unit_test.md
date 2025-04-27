import unittest

class MyRepository:
    def __init__(self):
        self.data = {}
        self.next_id = 1

    def add(self, item):
        item['id'] = self.next_id
        self.data[self.next_id] = item
        self.next_id += 1
        return item['id']
    
    def get(self, item_id):
        return self.data.get(item_id)
    
    def update(self, item_id, item):
      if item_id in self.data:
        item['id'] = item_id
        self.data[item_id] = item
        return True
      return False

    def delete(self, item_id):
      if item_id in self.data:
        del self.data[item_id]
        return True
      return False

class TestMyRepository(unittest.TestCase):
    def setUp(self):
        self.repo = MyRepository()
    
    def test_add_item(self):
        item_id = self.repo.add({'name': 'Test Item'})
        self.assertEqual(item_id, 1)
        retrieved_item = self.repo.get(item_id)
        self.assertEqual(retrieved_item['name'], 'Test Item')
    
    def test_get_item_not_found(self):
        retrieved_item = self.repo.get(99)
        self.assertIsNone(retrieved_item)

    def test_update_item(self):
        item_id = self.repo.add({'name': 'Old Name'})
        updated_item = {'name': 'New Name'}
        result = self.repo.update(item_id, updated_item)
        self.assertTrue(result)
        retrieved_item = self.repo.get(item_id)
        self.assertEqual(retrieved_item['name'], 'New Name')
    
    def test_update_item_not_found(self):
      updated_item = {'name': 'New Name'}
      result = self.repo.update(99, updated_item)
      self.assertFalse(result)

    def test_delete_item(self):
        item_id = self.repo.add({'name': 'To Delete'})
        result = self.repo.delete(item_id)
        self.assertTrue(result)
        retrieved_item = self.repo.get(item_id)
        self.assertIsNone(retrieved_item)

    def test_delete_item_not_found(self):
      result = self.repo.delete(99)
      self.assertFalse(result)

if __name__ == '__main__':
    unittest.main()