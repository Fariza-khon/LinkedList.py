# LinkedList.py
class LinkedList:
    class Item:
        def __init__(self, value):
            self.value = value
            self.next = None

    def __init__(self):
        self.head = None

    def append_begin(self, value):
        new_item = self.Item(value)
        new_item.next = self.head
        self.head = new_item

    def append_end(self, value):
        new_item = self.Item(value)
        if self.head is None:
            self.head = new_item
        else:
            current = self.head
            while current.next:
                current = current.next
            current.next = new_item

    def append_by_index(self, value, index):
        if index == 0:
            self.append_begin(value)
            return
        new_item = self.Item(value)
        current = self.head
        for _ in range(index - 1):
            if current is None:
                raise ValueError("Index out of bounds")
            current = current.next
        new_item.next = current.next
        current.next = new_item

    def __len__(self):
        count = 0
        current = self.head
        while current:
            count += 1
            current = current.next
        return count

    def remove_first(self):
        if self.head is None:
            raise ValueError("Cannot remove from an empty list")
        self.head = self.head.next

    def remove_last(self):
        if self.head is None:
            raise ValueError("Cannot remove from an empty list")
        if self.head.next is None:
            self.head = None
            return
        current = self.head
        while current.next.next:
            current = current.next
        current.next = None

    def remove_at(self, index):
        if index < 0:
            raise ValueError("Invalid index")
        if index == 0:
            self.remove_first()
            return
        current = self.head
        for _ in range(index - 1):
            if current is None or current.next is None:
                raise ValueError("Index out of bounds")
            current = current.next
        if current.next is None:
            raise ValueError("Index out of bounds")
        current.next = current.next.next

    def remove_first_value(self, value):
        if self.head is None:
            raise ValueError("List is empty")
        if self.head.value == value:
            self.head = self.head.next
            return
        current = self.head
        while current.next:
            if current.next.value == value:
                current.next = current.next.next
                return
            current = current.next
        raise ValueError("Value not found in the list")

    def remove_last_value(self, value):
        if self.head is None:
            raise ValueError("List is empty")
        if self.head.value == value:
            self.head = self.head.next
            return
        current = self.head
        while current.next:
            if current.next.value == value and current.next.next is None:
                current.next = None
                return
            if current.next.value == value:
                current.next = current.next.next
                return
            current = current.next
        raise ValueError("Value not found in the list")
