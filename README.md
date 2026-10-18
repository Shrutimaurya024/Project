# Python Project using oops

class Member:
    def __init__(self,name,member_id):
        self.name=name
        self.member_id=member_id
        self.borrowed_books=[]

    def borrow_book(self,book):
        if not book.is_borrowed:#ye tab chalega tab is_borrowed true ho jaye
            self.is_borrowed=True
            self.borrowed_books.append(book)
            print(f'{self.name} has borrowed book {book.title}')
        else:#is borrowed false rahega tab else chalega
            print(f'Sorry {book.title} is already borrowed')

    def return_book(self,book):
        if book in self.borrowed_books:
            book.is_borrowed=False
            self.borrowed_books.remove(book)
            print(f'{self.member_id} has return a book:{book.title}')
        else:
            print(f'book has not been borrowed')


    
class Book:

    def __init__(self,title,author,isbn):
        self.title=title
        self.author=author
        self.isbn=isbn
        self.is_borrowed=False


class Library:

    def __init__(self,name):
        self.name=name
        self.books=[]
        self.members=[]

    def add_book(self,title,author,isbn):#add book function yaha defined ho rha hai
        
        book=Book(title,author,isbn)#yaha Book class ka  object bana hai book jiske 3 arguments hai title author and isbn
        self.books.append(book)#yaha books naam ki list me book object ka data append kr diye
        print(f'Book {title} added successfully')

    def display_books(self):#here display book function is defined
        if not self.books:#if self.books is empty then this block will be executed
            print(f'no books are added in the library')
        else:#if self.books has values then this block will be executed
            for book in self.books:
                print(book)

    def add_member(self,name,member_id):#here add member function is defined
        member=Member(name,member_id)
        self.members.append(member)
        print(f'Member {name} is added successfully')
   
    def find_member(self,member_id):#here find member function is defined
        for member in self.members:
            if member.member_id==member_id:
                return member
        return None

    
    
    def find_isbn(self,isbn):#here find isbn function is defined
        for book in self.books:
            if book.isbn==isbn:
                return book
        return None
    def display_members(self):
        if not self.members:
            print(f'No members are added')
        
        else:
            for member in self.members:
                print(member)








def root():#root function yaha define ho rha
    library=Library("city central library")#library object hai Library clkass ka jisme ham argument pass kr rhe library ka name
    while True:
        print('Library Management System')
        print('1.Add Book')
        print('2.Display Books')
        print('3.Add Member')
        print('4.Borrow Book')
        print('5.Return Book')
        print('6.Display Members')
        print('7.Exit')

        choice=input("enter ur choice")
        if choice=="1":
            title=input("enter book title")
            author=input("enter book author")
            isbn=input("enter ISBN")
            library.add_book(title,author,isbn)#add book function yaha call ho raha hai
        
        elif choice=="2":
            library.display_books()#here display book function is called

        elif choice=="3":
            name=input("enter ur name")
            member_id=input("enter ur member id")
            library.add_member(name,member_id)#here add member function is called

        elif choice=="4":
            member_id=input("enter member id")
            isbn=input("enter isbn code")
            member=library.find_member(member_id)#here find member function is called
            print(f'Member added is:{member}')
            book=library.find_isbn(isbn)#here find isbn func is called
            print(f'Book added is:{book}')
            if member and book:
                member.borrow_book(book)

        elif choice=="5":
            member_id=input("enter member id")
            isbn=input("enter isbn code")
            member=library.find_member(member_id)#here find member function is called
         
            book=library.find_isbn(isbn)#here find isbn func is called
        
            if member and book:
                member.return_book(book)

        elif choice=="6":
            library.display_members()#here display member func is called

        elif choice=="7":
            print("thanku for using our library management system")
            break

        
        else:
            print("invalid choice")


if __name__=="__main__":#yaha root bfunction call ho rha hai
    root()
