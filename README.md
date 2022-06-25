# Linked_list

class LinkedList:
    class Node:
        def __init__(self,element = None ,node = None):
            self.element = element
            self.next = node
    def __init__(self):
        self.head = None # LinkedLIst의 시작 노드를 알고 있는 변수
        self.length = 0 # 요소의 개수를 저장할 변수
    def show(self):
        curr = self.head
        while curr != None:
            print(curr.element, end = '->')
            curr = curr.next
        print()
    
    # 데이터 삽입

    # 맨 앞에 삽입
    def insertFirst(self,*element):
        reverse_element = list(element)
        reverse_element.reverse()
        for i in element:
            newNode = self.Node(i, self.head)
            self.head = newNode
            break
        for i in reverse_element[:-1]:
            newNode2 = self.Node(i, self.head.next)
            self.head.next = newNode2
        self.length += len(element)
        
            
    # 맨 뒤에 삽입

    def insertLast(self, *element):

        if self.head == None:
            self.insertFirst(element)
            return
        
        # 마지막노드를 찾아야 한다. 

        curr = self.head
        while curr.next != None:
            curr = curr.next
        
        # 반복이 종료되면 tail이 curr에 담긴다.            
        reverse_element = list(element)
        reverse_element.reverse()
        for i in reverse_element:
            newNode = self.Node(i,curr.next)
            curr.next = newNode
        self.length += len(element)
        

        # 중간에 삽입
    def insert(self,idx,*element):
        if idx < 0 or idx > self.length:
        # print('인덱스 범위 벗어남')
        # return
            raise IndexError('인덱스 벗어남')

        # idx가 0이라면
        if idx == 0:
            self.insertFirst(element)
            return
        
        # 삽입할 위치 이전 노드를 찾아야 한다. 

        curr = self.head
        for i in range(idx-1):
            curr = curr.next
            
        reverse_element = list(element)
        reverse_element.reverse()
        for i in reverse_element:
            newNode = self.Node(i,curr.next)
            curr.next = newNode
        self.length += len(element)
    
    # 삭제
    def removeFirst(self):
        if self.head == None:  # 데이터가 한개도 없다면
            return
        
        self.head = self.head.next
        self.length -= 1
    
    def remove(self,idx):
        if idx < 0 or idx >= self.length:
        # print('인덱스 벗어남')
        # return
            raise IndexError('인덱스 벗어남')
        
        if idx == 0:
            self.removeFirst()
            return
        
        curr = self.head
        for i in range(idx):
            prev = curr
            curr = curr.next

        prev.next = curr.next
        self.length -= 1

    # 검색, 인덱스 번호로 검색
    def select(self, idx):
        # idx 유효성 검사
        if idx < 0 or idx >= self.length:
            # print('인덱스 벗어남')
            # return
            raise IndexError('인덱스 벗어남')
        curr = self.head
        for i in range(idx):
            curr = curr.next

        return curr.element

    # 수정
    def update(self,idx, element):
        # 유효성 검사
        if idx < 0 or idx >= self.length:
        # print('인덱스 벗어남')
        # return
            raise IndexError('인덱스 벗어남')
        curr = self.head
        for i in range(idx):
            curr = curr.next
        curr.element = element
        
        # 아마 가산변수 넣어주고 반복문으로 반복해서 값들마다 각각 변수에 넣어줘야할듯
a = LinkedList()
a.insertFirst(1,20,30)
a.show()
a.insertLast(100,200,300)
a.insertLast(400)
a.insertFirst(1000)
a.show()
a.insert(2,55,22)
a.show()
